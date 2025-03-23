# Web Scraping with Beautiful Soup (Part 3)
## Scraping the Illinois General Assembly
Believe it or not, those are really the fundamental tools you need to scrape a website. Once you spend more time familiarizing yourself with HTML and CSS, 
then it's simply a matter of understanding the structure of a particular website and intelligently applying the tools of Beautiful Soup and Python.
Let's apply these skills to scrape the Illinois 98th General Assembly.
Specifically, our goal is to scrape information on each senator, including their name, district, and party.
### Scrape and Soup the Webpage
Let's scrape and parse the webpage, using the tools we learned in the previous section.
~~~
# Make a GET request
req = requests.get('http://www.ilga.gov/senate/default.asp?GA=98')
# Read the content of the server’s response
src = req.text
# Soup it
soup = BeautifulSoup(src, "lxml")
~~~
~~~
0.2s
~~~
### Search for the Table Elements
Our goal is to obtain the elements in the table on the webpage. 
Remember: rows are identified by the tr tag. Let's use find_all to obtain these elements.
~~~
# Get all table row elements
rows = soup.find_all("tr")
len(rows)
~~~
~~~
…73
~~~
⚠️ **Warning**: Keep in mind: find_all gets all the elements with the tr tag. 
We only want some of them. If we use the 'Inspect' function in Google Chrome and look carefully, 
then we can use some CSS selectors to get just the rows we're interested in. 
Specifically, we want the inner rows of the table:
~~~
# Returns every ‘tr tr tr’ css selector in the page
rows = soup.select('tr tr tr')
for row in rows[:5]:
print(row, '\n')
~~~
~~~
<tr><td colspan="5">
<span class="heading">Illinois State Senators</span>
<span class="italics">  98th  General Assembly</span><br/>
<!-- 3/2/09 temp comment out until fixed for GA specific-->
<!-- add 97th ga currently no info -->
<a href="98GA_Senate_Leadership.pdf">Leadership</a> <a href="98th_Senate_Officers.pdf">Officers</a> <a href="98GA_Senate_Seating_Chart.pdf">Senate Seating Chart</a>  <span class="content"><b>Democrats:</b> 40   <b>Republicans:</b> 19</span><br/>
</td></tr> 
<tr>
<td class="header" width="45%"><a class="filetab" href="javascript:Sort('LastName','',98);" title="Sort by Senator">Senator</a></td>
<td align="center" class="header" width="15%">Bills</td>
<td align="center" class="header" width="10%">Committees</td>
<td align="center" class="header" width="15%"><a class="filetab" href="javascript:Sort('DistrictNumber','',98);" title="Sort by District">District</a></td>
<td align="center" class="header" width="15%"><a class="filetab" href="javascript:Sort('Party','',98);" title="Sort by Party">Party</a></td>
</tr> 
<tr><td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td><td align="center" bgcolor="white" class="detail" width="15%">32</td><td align="center" bgcolor="white" class="detail" width="15%">R</td></tr> 

<tr><td bgcolor="EBEBEB" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=2018">Jason A. Barickman</a></td><td align="center" bgcolor="EBEBEB" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=2018">Bills</a></td><td align="center" bgcolor="EBEBEB" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=2018">Committees</a></td><td align="center" bgcolor="EBEBEB" class="detail" width="15%">53</td><td align="center" bgcolor="EBEBEB" class="detail" width="15%">R</td></tr> 

<tr><td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=2272">Scott M Bennett</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=2272">Bills</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=2272">Committees</a></td><td align="center" bgcolor="white" class="detail" width="15%">52</td><td align="center" bgcolor="white" class="detail" width="15%">D</td></tr>
~~~
It looks like we want everything after the first two rows. Let's work with a single row to start, and build our loop from there.
~~~
example_row = rows[2]
print(example_row.prettify())
~~~
~~~
<tr>
 <td bgcolor="white" class="detail" width="40%">
  <a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">
   Pamela J. Althoff
  </a>
 </td>
 <td align="center" bgcolor="white" class="detail" width="15%">
  <a href="SenatorBills.asp?GA=98&amp;MemberID=1911">
   Bills
  </a>
 </td>
 <td align="center" bgcolor="white" class="detail" width="15%">
  <a href="SenCommittees.asp?GA=98&amp;MemberID=1911">
   Committees
  </a>
 </td>
 <td align="center" bgcolor="white" class="detail" width="15%">
  32
 </td>
 <td align="center" bgcolor="white" class="detail" width="15%">
  R
 </td>
</tr>
~~~

Let's break this row down into its component cells/columns using the select method with CSS selectors. 
Looking closely at the HTML, there are a couple of ways we could do this.
  - We could identify the cells by their tag td.
  - We could use the the class name .detail.
  - We could combine both and use the selector td.detail.
~~~
for cell in example_row.select('td'):
      print(cell)
print()
for cell in example_row.select('.detail'):
    	print(cell)
print()
 for cell in example_row.select('td.detail'):
  	  print(cell)
print()
~~~
~~~
<td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td>
<td align="center" bgcolor="white" class="detail" width="15%">32</td>
<td align="center" bgcolor="white" class="detail" width="15%">R</td>

<td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td>
<td align="center" bgcolor="white" class="detail" width="15%">32</td>
<td align="center" bgcolor="white" class="detail" width="15%">R</td>

<td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td>
<td align="center" bgcolor="white" class="detail" width="15%">32</td>
<td align="center" bgcolor="white" class="detail" width="15%">R</td><td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td>
<td align="center" bgcolor="white" class="detail" width="15%">32</td>
<td align="center" bgcolor="white" class="detail" width="15%">R</td>

<td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td>
<td align="center" bgcolor="white" class="detail" width="15%">32</td>
<td align="center" bgcolor="white" class="detail" width="15%">R</td>
~~~
We can confirm that these are all the same.
~~~
assert example_row.select('td') == example_row.select('.detail') == example_row.select('td.detail')
~~~
Let's use the selector td.detail to be as specific as possible.
~~~
# Select only those 'td' tags with class 'detail' 
detail_cells = example_row.select('td.detail')
detail_cells
~~~
~~~
[<td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td>,
 <td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td>,
 <td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td>,
 <td align="center" bgcolor="white" class="detail" width="15%">32</td>,
 <td align="center" bgcolor="white" class="detail" width="15%">R</td>]
~~~
Most of the time, we're interested in the actual text of a website, not its tags. Recall that to get the text of an HTML element, we use the text member:
~~~
# Keep only the text in each of those cells
row_data = [cell.text for cell in detail_cells]
print(row_data)
~~~
~~~
['Pamela J. Althoff', 'Bills', 'Committees', '32', 'R']
~~~
Looks good! Now we just use our basic Python knowledge to get the elements of this list that we want. 
Remember, we want the senator's name, their district, and their party.
~~~
print(row_data[0]) # Name
print(row_data[3]) # District
print(row_data[4]) # Party
~~~
~~~
Pamela J. Althoff
32
R
~~~
## Getting Rid of Junk Rows
We saw at the beginning that not all of the rows we got actually correspond to a senator. 
We'll need to do some cleaning before we can proceed forward. Take a look at some examples:
~~~
print('Row 0:\n', rows[0], '\n')
print('Row 1:\n', rows[1], '\n')
print('Last Row:\n', rows[-1])
~~~
~~~
Row 0:
 <tr><td colspan="5">
<span class="heading">Illinois State Senators</span>
<span class="italics">  98th  General Assembly</span><br/>
<!-- 3/2/09 temp comment out until fixed for GA specific-->
<!-- add 97th ga currently no info -->
<a href="98GA_Senate_Leadership.pdf">Leadership</a> <a href="98th_Senate_Officers.pdf">Officers</a> <a href="98GA_Senate_Seating_Chart.pdf">Senate Seating Chart</a>  <span class="content"><b>Democrats:</b> 40   <b>Republicans:</b> 19</span><br/>
</td></tr> 
Row 1:
 <tr>
<td class="header" width="45%"><a class="filetab" href="javascript:Sort('LastName','',98);" title="Sort by Senator">Senator</a></td>
<td align="center" class="header" width="15%">Bills</td>
<td align="center" class="header" width="10%">Committees</td>
<td align="center" class="header" width="15%"><a class="filetab" href="javascript:Sort('DistrictNumber','',98);" title="Sort by District">District</a></td>
<td align="center" class="header" width="15%"><a class="filetab" href="javascript:Sort('Party','',98);" title="Sort by Party">Party</a></td>
</tr> 

Last Row:
 <tr>
<td align="left" class="footer" width="107">  <img alt="Legislative Information System logo" height="45" src="/images/lislogo.jpg" width="100"/></td>
<td align="" class="footer" valign="top" width="100%">This site is maintained for the Illinois General Assembly 
by the<br/>Legislative Information System, 705 Stratton Building, Springfield, Illinois 62706<br/>
<a class="links" href="mailto:webmaster@ilga.gov?subject=Email from ILGA Web" style="font-size:8px">
      Contact ILGA Webmaster</a>
</td>
</tr>
~~~
When we write our for loop, we only want it to apply to the relevant rows. So we'll need to filter out the irrelevant rows. 
The way to do this is to compare some of these to the rows we do want, see how they differ, and then formulate that in a conditional.
As you can imagine, there a lot of possible ways to do this, and it'll depend on the website. We'll show some here to give you an idea of how to do this.
~~~
# Bad rows
print(len(rows[0]))
print(len(rows[1]))
~~~
~~~
# Good rows
print(len(rows[2]))
print(len(rows[3]))
~~~
~~~
1
11
5
5
~~~
Perhaps good rows have a length of 5. Let's check:
~~~
good_rows = [row for row in rows if len(row) == 5]
# Let's check some rows
print(good_rows[0], '\n')
print(good_rows[-2], '\n')
print(good_rows[-1])
~~~
~~~
<tr><td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td><td align="center" bgcolor="white" class="detail" width="15%">32</td><td align="center" bgcolor="white" class="detail" width="15%">R</td></tr> 

<tr><td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=2035">Patricia Van Pelt</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=2035">Bills</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=2035">Committees</a></td><td align="center" bgcolor="white" class="detail" width="15%">5</td><td align="center" bgcolor="white" class="detail" width="15%">D</td></tr> 

<tr>
<td align="left" class="footer" width="107">  <img alt="Legislative Information System logo" height="45" src="/images/lislogo.jpg" width="100"/></td>
<td align="" class="footer" valign="top" width="100%">This site is maintained for the Illinois General Assembly 
by the<br/>Legislative Information System, 705 Stratton Building, Springfield, Illinois 62706<br/>
<a class="links" href="mailto:webmaster@ilga.gov?subject=Email from ILGA Web" style="font-size:8px">
      Contact ILGA Webmaster</a>
</td>
</tr>
~~~
We found a footer row in our list that we'd like to avoid. Let's try something else:
~~~
rows[2].select('td.detail')
~~~
~~~
[<td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td>,
 <td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td>,
 <td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td>,
 <td align="center" bgcolor="white" class="detail" width="15%">32</td>,
 <td align="center" bgcolor="white" class="detail" width="15%">R</td>]
~~~
~~~
# Bad row
print(rows[-1].select('td.detail'), '\n')
# Good row
print(rows[5].select('td.detail'), '\n')
# How about this?
good_rows = [row for row in rows if row.select('td.detail')]
print("Checking rows...\n")
print(good_rows[0], '\n')
print(good_rows[-1])
~~~
~~~
[] 
[<td bgcolor="EBEBEB" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=2022">Jennifer Bertino-Tarrant</a></td>, <td align="center" bgcolor="EBEBEB" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=2022">Bills</a></td>, <td align="center" bgcolor="EBEBEB" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=2022">Committees</a></td>, <td align="center" bgcolor="EBEBEB" class="detail" width="15%">49</td>, <td align="center" bgcolor="EBEBEB" class="detail" width="15%">D</td>] 
Checking rows...
<tr><td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td><td align="center" bgcolor="white" class="detail" width="15%">32</td><td align="center" bgcolor="white" class="detail" width="15%">R</td></tr> 
<tr><td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=2035">Patricia Van Pelt</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=2035">Bills</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=2035">Committees</a></td><td align="center"
~~~
Looks like we found something that worked!

 ***
 ***
# Arrastrar la Web con Bonita Disolución (Parte 3)
## Arrastrando la Asamblea General de Illinois
Aunque parezca increíble, estas son las herramientas fundamentales para arrastrar un sitio web. Una vez que dediques más tiempo a familiarizarte con HTML y CSS, simplemente será cuestión de comprender la estructura de un sitio web en particular y aplicar inteligentemente las herramientas de Beautiful Soup y Python.
Apliquemos estas habilidades para arrastrar la 98.ª Asamblea General de Illinois.
En concreto, nuestro objetivo es arrastrar información sobre cada senador, incluyendo su nombre, distrito y partido.
### Arrastrar y Disolver la página web
Arrastrar y Analizar la página web con las herramientas que aprendimos en la sección anterior.
~~~
# Make a GET request
req = requests.get('http://www.ilga.gov/senate/default.asp?GA=98')
# Read the content of the server’s response
src = req.text
# Soup it
soup = BeautifulSoup(src, "lxml")
~~~
~~~
0.2s
~~~
### Buscar los elementos de la tabla
Nuestro objetivo es obtener los elementos de la tabla en la página web. Recuerda: las filas se identifican con la etiqueta tr. 
Usaremos find_all para obtener estos elementos.
~~~
# Get all table row elements
rows = soup.find_all("tr")
len(rows)
~~~
~~~
…73
~~~
⚠️ **Advertencia**: Recuerda: find_all obtiene todos los elementos con la etiqueta tr. Solo necesitamos algunos. 
Si usamos la función "Inspeccionar" en Google Chrome y observamos con atención, podemos usar selectores CSS para obtener 
solo las filas que nos interesan. En concreto, queremos las filas internas de la tabla:
~~~
# Returns every ‘tr tr tr’ css selector in the page
rows = soup.select('tr tr tr')
for row in rows[:5]:
print(row, '\n')
~~~
~~~
<tr><td colspan="5">
<span class="heading">Illinois State Senators</span>
<span class="italics">  98th  General Assembly</span><br/>
<!-- 3/2/09 temp comment out until fixed for GA specific-->
<!-- add 97th ga currently no info -->
<a href="98GA_Senate_Leadership.pdf">Leadership</a> <a href="98th_Senate_Officers.pdf">Officers</a> <a href="98GA_Senate_Seating_Chart.pdf">Senate Seating Chart</a>  <span class="content"><b>Democrats:</b> 40   <b>Republicans:</b> 19</span><br/>
</td></tr> 
<tr>
<td class="header" width="45%"><a class="filetab" href="javascript:Sort('LastName','',98);" title="Sort by Senator">Senator</a></td>
<td align="center" class="header" width="15%">Bills</td>
<td align="center" class="header" width="10%">Committees</td>
<td align="center" class="header" width="15%"><a class="filetab" href="javascript:Sort('DistrictNumber','',98);" title="Sort by District">District</a></td>
<td align="center" class="header" width="15%"><a class="filetab" href="javascript:Sort('Party','',98);" title="Sort by Party">Party</a></td>
</tr> 
<tr><td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td><td align="center" bgcolor="white" class="detail" width="15%">32</td><td align="center" bgcolor="white" class="detail" width="15%">R</td></tr> 

<tr><td bgcolor="EBEBEB" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=2018">Jason A. Barickman</a></td><td align="center" bgcolor="EBEBEB" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=2018">Bills</a></td><td align="center" bgcolor="EBEBEB" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=2018">Committees</a></td><td align="center" bgcolor="EBEBEB" class="detail" width="15%">53</td><td align="center" bgcolor="EBEBEB" class="detail" width="15%">R</td></tr> 

<tr><td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=2272">Scott M Bennett</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=2272">Bills</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=2272">Committees</a></td><td align="center" bgcolor="white" class="detail" width="15%">52</td><td align="center" bgcolor="white" class="detail" width="15%">D</td></tr> 
~~~
Parece que queremos todo lo que queda después de las dos primeras filas. Empecemos con una sola fila y construyamos nuestro bucle a partir de ahí.
~~~
example_row = rows[2]
print(example_row.prettify())
~~~

Desglosemos esta fila en sus celdas/columnas mediante el método select con los métodos CSS. Si analizamos el HTML con atención, 
hay un par de maneras de hacerlo.
  - Podríamos identificar las celdas por su etiqueta td.
  - Podríamos usar el nombre de clase .detail.
  - Podríamos combinar ambos y usar el selector td.detail.
~~~
for cell in example_row.select('td'):
      print(cell)
print()
for cell in example_row.select('.detail'):
    	print(cell)
print()
 for cell in example_row.select('td.detail'):
  	  print(cell)
print()
~~~
~~~
<td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td>
<td align="center" bgcolor="white" class="detail" width="15%">32</td>
<td align="center" bgcolor="white" class="detail" width="15%">R</td>

<td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td>
<td align="center" bgcolor="white" class="detail" width="15%">32</td>
<td align="center" bgcolor="white" class="detail" width="15%">R</td>

<td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td>
<td align="center" bgcolor="white" class="detail" width="15%">32</td>
<td align="center" bgcolor="white" class="detail" width="15%">R</td><td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td>
<td align="center" bgcolor="white" class="detail" width="15%">32</td>
<td align="center" bgcolor="white" class="detail" width="15%">R</td>

<td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td>
<td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td>
<td align="center" bgcolor="white" class="detail" width="15%">32</td>
<td align="center" bgcolor="white" class="detail" width="15%">R</td>
~~~
Podemos confirmar que todas son iguales
~~~
assert example_row.select('td') == example_row.select('.detail') == example_row.select('td.detail')
~~~
Utilicemos el selector td.detail para ser lo más específicos posibles.
~~~
# Select only those 'td' tags with class 'detail' 
detail_cells = example_row.select('td.detail')
detail_cells
~~~
~~~
[<td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td>,
 <td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td>,
 <td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td>,
 <td align="center" bgcolor="white" class="detail" width="15%">32</td>,
 <td align="center" bgcolor="white" class="detail" width="15%">R</td>]
~~~
La mayoría de las veces, nos interesa el texto real de un sitio web, no sus etiquetas. 
Recordemos que para obtener el texto de un elemento HTML, usamos el text member:
~~~
# Keep only the text in each of those cells
row_data = [cell.text for cell in detail_cells]
print(row_data)
~~~
~~~
['Pamela J. Althoff', 'Bills', 'Committees', '32', 'R']
~~~
¡Se ve bien! Ahora solo necesitamos usar nuestros conocimientos básicos de Python para obtener los elementos de esta lista que necesitamos. 
Recuerda: queremos el nombre del senador, su distrito y su partido.
~~~
print(row_data[0]) # Name
print(row_data[3]) # District
print(row_data[4]) # Party
~~~
~~~
Pamela J. Althoff
32
R
~~~
### Eliminando las filas basura
Vimos al principio que no todas las filas que obtuvimos corresponden a un senador. 
Tendremos que hacer limpieza antes de continuar. Veamos algunos ejemplos:
~~~
print('Row 0:\n', rows[0], '\n')
print('Row 1:\n', rows[1], '\n')
print('Last Row:\n', rows[-1])
~~~
~~~
Row 0:
 <tr><td colspan="5">
<span class="heading">Illinois State Senators</span>
<span class="italics">  98th  General Assembly</span><br/>
<!-- 3/2/09 temp comment out until fixed for GA specific-->
<!-- add 97th ga currently no info -->
<a href="98GA_Senate_Leadership.pdf">Leadership</a> <a href="98th_Senate_Officers.pdf">Officers</a> <a href="98GA_Senate_Seating_Chart.pdf">Senate Seating Chart</a>  <span class="content"><b>Democrats:</b> 40   <b>Republicans:</b> 19</span><br/>
</td></tr>
Row 1:
 <tr>
<td class="header" width="45%"><a class="filetab" href="javascript:Sort('LastName','',98);" title="Sort by Senator">Senator</a></td>
<td align="center" class="header" width="15%">Bills</td>
<td align="center" class="header" width="10%">Committees</td>
<td align="center" class="header" width="15%"><a class="filetab" href="javascript:Sort('DistrictNumber','',98);" title="Sort by District">District</a></td>
<td align="center" class="header" width="15%"><a class="filetab" href="javascript:Sort('Party','',98);" title="Sort by Party">Party</a></td>
</tr> 

Last Row:
 <tr>
<td align="left" class="footer" width="107">  <img alt="Legislative Information System logo" height="45" src="/images/lislogo.jpg" width="100"/></td>
<td align="" class="footer" valign="top" width="100%">This site is maintained for the Illinois General Assembly 
by the<br/>Legislative Information System, 705 Stratton Building, Springfield, Illinois 62706<br/>
<a class="links" href="mailto:webmaster@ilga.gov?subject=Email from ILGA Web" style="font-size:8px">
      Contact ILGA Webmaster</a>
</td>
</tr>
~~~
Al escribir nuestro bucle for, queremos que solo se aplique a las filas relevantes. 
Por lo tanto, debemos filtrar las filas irrelevantes. Para ello, comparamos algunas de estas con las filas que necesitamos, 
observamos sus diferencias y luego formulamos esto en una condición.
Como puedes imaginar, hay muchas maneras de hacerlo, y dependerá del sitio web. 
Aquí te mostraremos algunas para que te hagas una idea de cómo hacerlo.
~~~
# Bad rows
print(len(rows[0]))
print(len(rows[1]))
# Good rows
print(len(rows[2]))
print(len(rows[3]))
~~~
~~~
1
11
5
5
~~~
Quizás las filas buenas tengan una longitud de 5. Comprobémoslo:
~~~
good_rows = [row for row in rows if len(row) == 5]
# Let's check some rows
print(good_rows[0], '\n')
print(good_rows[-2], '\n')
print(good_rows[-1])
~~~
~~~
<tr><td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td><td align="center" bgcolor="white" class="detail" width="15%">32</td><td align="center" bgcolor="white" class="detail" width="15%">R</td></tr> 

<tr><td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=2035">Patricia Van Pelt</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=2035">Bills</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=2035">Committees</a></td><td align="center" bgcolor="white" class="detail" width="15%">5</td><td align="center" bgcolor="white" class="detail" width="15%">D</td></tr> 

<tr>
<td align="left" class="footer" width="107">  <img alt="Legislative Information System logo" height="45" src="/images/lislogo.jpg" width="100"/></td>
<td align="" class="footer" valign="top" width="100%">This site is maintained for the Illinois General Assembly 
by the<br/>Legislative Information System, 705 Stratton Building, Springfield, Illinois 62706<br/>
<a class="links" href="mailto:webmaster@ilga.gov?subject=Email from ILGA Web" style="font-size:8px">
      Contact ILGA Webmaster</a>
</td>
</tr>
~~~
Encontramos una fila de pie de página en nuestra lista que queremos evitar. Probemos algo diferente:
~~~
rows[2].select('td.detail') 
~~~
~~~
[<td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td>,
 <td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td>,
 <td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td>,
 <td align="center" bgcolor="white" class="detail" width="15%">32</td>,
 <td align="center" bgcolor="white" class="detail" width="15%">R</td>]
~~~
~~~
# Bad row
print(rows[-1].select('td.detail'), '\n')
# Good row
print(rows[5].select('td.detail'), '\n')
# How about this?
good_rows = [row for row in rows if row.select('td.detail')]
print("Checking rows...\n")
print(good_rows[0], '\n')
print(good_rows[-1])
~~~
~~~
[] 
[<td bgcolor="EBEBEB" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=2022">Jennifer Bertino-Tarrant</a></td>, <td align="center" bgcolor="EBEBEB" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=2022">Bills</a></td>, <td align="center" bgcolor="EBEBEB" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=2022">Committees</a></td>, <td align="center" bgcolor="EBEBEB" class="detail" width="15%">49</td>, <td align="center" bgcolor="EBEBEB" class="detail" width="15%">D</td>] 
Checking rows...
<tr><td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=1911">Pamela J. Althoff</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=1911">Bills</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=1911">Committees</a></td><td align="center" bgcolor="white" class="detail" width="15%">32</td><td align="center" bgcolor="white" class="detail" width="15%">R</td></tr> 
<tr><td bgcolor="white" class="detail" width="40%"><a class="notranslate" href="/senate/Senator.asp?GA=98&amp;MemberID=2035">Patricia Van Pelt</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenatorBills.asp?GA=98&amp;MemberID=2035">Bills</a></td><td align="center" bgcolor="white" class="detail" width="15%"><a href="SenCommittees.asp?GA=98&amp;MemberID=2035">Committees</a></td><td align="center"
~~~
¡Parece que encontramos algo que funcionó!

