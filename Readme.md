
[![Test Coverage](https://api.codeclimate.com/v1/badges/bc6194d22404dbf244c3/test_coverage)](https://codeclimate.com/github/anshulgoyal15/imdb-scrapper/test_coverage)
<h1>IMDB SCRAPPER</h1>
This is one stop tool/lib for getting any type of data from imdb site,eg you can get cast
of a movie or awards won by movie and some of it's basic info.All the images function provide images with title and poster of high quality.
Every function in this lib is async it returns a promise.The module is made to be modular for different function like it provide four function:
<ul>
<li>scrapper(id) id here reffer to imdbID like:'tt1825683'. This function provide some basic data like genre,runtime,plot etc</li>
<li>awardsPage(id) id here reffer to imdbID like:'tt1825683'.This function provide awards won by movies by default it provide first three awards or most rated ones</li>
<li>getCast(id,n) id here reffer to imdbID like:'tt1825683' n is optional it specify the no. of actors required by default it is set to 20. This function provide cast of the movies </li>
<li> getFull(id) id here reffer to imdbID like:'tt1825683.This function is the combination of above three,but with it's configuration is set to default </li>
</ul>
<h2>Using Above function in Different PNC</h2>
If awards and cast is only required,

```javascript
const funs=[awardsPage('tt1825683'),getCast('tt1825683',14)];
Promise.all(funs).then((data)=>{
    return {...data[0],...data[1]}
}).then((movieDetails)=>{
    console.log(movieDetails)
})
```
<h3>To install</h3>
```
npm install --save imdb-scrapper
```
<h1>SEACRH APIS</h1>
The most important aspect of any movie site is search .This module provide two search Stragey:
<ul>
<li>serach(term,n) term reprensts the search query n signify the required number of results.The 
function provide serach results from all the genre</li>
<li>simpleSearch(term) term reprensts the search query This function is faster as it directly uses 
the ajax calls made by imdb page and can be suited for auto complete feature</li>
</ul>
<h1>Trending movies</h1>
This section is not provided by any other api or scrapper including cast and awards.
There are two different ways of scrapping provide by this lib:
<ul>
<li>getTrending(n) n is optional parameter giving the count of result required.This function provide
 the trending movies known as 'trending 250' on imdb website</li>
<li>getTrendingGenre(genre,n) n is optional parameter giving the count of result required.This function provide results sorted on the basis of genre </li>
</ul>

<h1>EXAMPLES</h1>
<h2>SCRAPPER</h2>

```javascript

const {scrapper}=require('imdb-scrapper');


scrapper('tt1825683').then((movieDetails)=>{
    console.log(movieDetails)

})
```
output:
```
{ title: 'Black Panther (2018)',
  runtime: '2h 14min',
  year: '2018',
  story: 'After the events of Captain America: Civil War, King Challa returns home to the reclusive,
  technologically advanced African nation of Wakanda to serve as his countrys new leader. However,
  Challa soon finds that he is challenged for the throne from factions within his own country.
  When two foes conspire to destroy Wakanda, the hero known as Black Panther must team up with
  C.I.A. agent Everett K. Ross and members of the Dora Milaje, Wakandan special forces, to prevent Wakanda
   from being dragged into a world war.',
  director: 'Ryan Coogler',
  writer: 'Ryan Coogler',
  genre: [ ' Action ', ' Adventure ', ' Sci-Fi' ],
  rating: '7.8',
  poster: 
  'https://ia.media-imdb.com/images/M/MV5BMTg1MTY2MjYzNV5BMl5BanBnXkFtZTgwMTc4NTMwNDI@._V1_UX182_CR0,
  0,182,268_AL__QL50.jpg',
  
   }


```
<h2>AWARDSPAGE</h2>

```javascript

const {scrapper}=require('imdb-scrapper');

awardsPage('tt5580390').then((movieDetails)=>{
    console.log(movieDetails)

})
```

output:
```
{ Oscar:
   [ { category: 'Best Achievement in Directing',
       wonBy: 'Guillermo del Toro' },
     { category: 'Best Motion Picture of the Year',
       wonBy: 'Guillermo del Toro' },
     { category: 'Best Achievement in Music Written for Motion Pictures (Original Score)',
       wonBy: 'Alexandre Desplat' },
     { category: 'Best Achievement in Production Design',
       wonBy: 'Paul D. Austerberry' } ],
  'Golden Globe':
   [ { category: 'Best Director - Motion Picture',
       wonBy: 'Guillermo del Toro' },
     { category: 'Best Original Score - Motion Picture',
       wonBy: 'Alexandre Desplat' } ],
  'BAFTA Film Award':
   [ { category: 'Best Production Design',
       wonBy: 'Paul D. Austerberry' },
     { category: 'Original Music', wonBy: 'Alexandre Desplat' } ] }

```
<h2>GETFULL</h2>


```javascript
const {scrapper,awardsPage,getFull}=require('imdb-scrapper');

getFull('tt2395427').then((movieDetails)=>{
    console.log(movieDetails)

})
```
output:
```
{ title: 'Avengers: Age of Ultron (2015)',
  runtime: '2h 21min',
  year: '2015',
  story: 'ony Stark creates the Ultron Program to protect the world, but when the peacekeeping 
  program becomes hostile, he Avengers go into action to try and defeat a virtually impossible enemy 
  together. Earths mightiest heroes must come together once again to protect the world from global 
  extinction.                Written byapplenatalia9            ',
  director: 'Joss Whedon',
  writer: 'Joss Whedon',
  genre: [ ' Action ', ' Adventure ', ' Sci-Fi' ],
  rating: '7.4',
  poster: 
  'https://ia.media-imdb.com/images/M/MV5BMTM4OGJmNWMtOTM4Ni00NTE3LTg3MDItZmQxYjc4N2JhNmUxXkEyXkFqcGde
  QXVyNTgzMDMzMTg@._V1_UX182_CR0,0,182,268_AL__QL50.jpg',
  'Saturn Award':
   [ { category: 'Best Costume Design', wonBy: 'Alexandra Byrne' } ],
  Annie:
   [ { category: 'Outstanding Achievement in Animated Effects in a Live Action Production',
       wonBy: 'Michael Balog' } ],
  'AACTA Award':
   [ { category: 'Best Visual Effects or Animation',
       wonBy: 'Christopher Townsend' } ],
  cast:
   [ { name: 'Robert Downey Jr.',
       image: 
       'https://ia.media-imdb.com/images/M/MV5BNzg1MTUyNDYxOF5BMl5BanBnXkFtZTgwNTQ4MTE2MjE@.
       _V1_UX75_CR0,0,75,109_AL_.jpg',
       role: 'Tony Stark/Iron Man' },
     { name: 'Chris Hemsworth',
       image: 
       'https://ia.media-imdb.com/images/M/MV5BOTU2MTI0NTIyNV5BMl5BanBnXkFtZTcwMTA4Nzc3OA@@.
       _V1_UX75_CR0,0,75,109_AL_.jpg',
       role: 'Thor' },
     { name: 'Mark Ruffalo',
       image: 
       'https://ia.media-imdb.
       com/images/M/MV5BNDQyNzMzZTMtYjlkNS00YzFhLWFhMTctY2M4YmQ1NmRhODBkXkEyXkFqcGdeQXVyNjcyNzgyOTE@.
       _V1_UY109_CR6,0,75,109_AL_.jpg',
       role: 'Bruce Banner/Hulk' },
     { name: 'Chris Evans',
       image: 
       'https://ia.media-imdb.com/images/M/MV5BMTU2NTg1OTQzMF5BMl5BanBnXkFtZTcwNjIyMjkyMg@@.
       _V1_UY109_CR1,0,75,109_AL_.jpg',
       role: 'Steve Rogers/Captain America' },
     { name: 'Scarlett Johansson',
       image: 
       'https://ia.media-imdb.com/images/M/MV5BMTM3OTUwMDYwNl5BMl5BanBnXkFtZTcwNTUyNzc3Nw@@.
       _V1_UY109_CR7,0,75,109_AL_.jpg',
       role: 'Natasha Romanoff/Black Widow' },
     { name: 'Jeremy Renner',
       image: 
       'https://ia.media-imdb.com/images/M/MV5BOTk2NDc2ODgzMF5BMl5BanBnXkFtZTcwMTMzOTQ4Nw@@.
       _V1_UX75_CR0,0,75,109_AL_.jpg',
       role: 'Clint Barton/Hawkeye' },
     { name: 'James Spader',
       image: 
       'https://ia.media-imdb.com/images/M/MV5BMTQ3MTQ5NjY5Ml5BMl5BanBnXkFtZTgwMTY0NzU5MDE@.
       _V1_UY109_CR4,0,75,109_AL_.jpg',
       role: 'Ultron' },
     { name: 'Samuel L. Jackson',
       image: 
       'https://ia.media-imdb.com/images/M/MV5BMTQ1NTQwMTYxNl5BMl5BanBnXkFtZTYwMjA1MzY1._V1_UX75_CR0,
       0,75,109_AL_.jpg',
       role: 'Nick Fury' },
     { name: 'Don Cheadle',
       image: 
       'https://ia.media-imdb.com/images/M/MV5BNDMxNDM3MzY5N15BMl5BanBnXkFtZTcwMjkzOTY4MQ@@.
       _V1_UY109_CR5,0,75,109_AL_.jpg',
       role: 'James Rhodes/War Machine' },
     { name: 'Aaron Taylor-Johnson',
       image: 
       'https://ia.media-imdb.com/images/M/MV5BMzE5MzI0MzY2OF5BMl5BanBnXkFtZTgwODE3MTk4MTE@.
       _V1_UY109_CR4,0,75,109_AL_.jpg',
       role: 'Pietro Maximoff/Quicksilver' },
     { name: 'Elizabeth Olsen',
       image: '
       https://ia.media-imdb.com/images/M/MV5BMjEzMjA0ODk1OF5BMl5BanBnXkFtZTcwMTA4ODM3OQ@@.
       _V1_UY109_CR1,0,75,109_AL_.jpg',
       role: 'Wanda Maximoff/Scarlet Witch' },
     { name: 'Paul Bettany',
       image: '
       https://ia.media-imdb.com/images/M/MV5BMjEwODg1MTA5Ml5BMl5BanBnXkFtZTcwNDQwMTQxMw@@.
       _V1_UY109_CR3,0,75,109_AL_.jpg',
       role: 'Jarvis/Vision' },
     { name: 'Cobie Smulders',
       image: '
       https://ia.media-imdb.com/images/M/MV5BMTkzNTUyMTczM15BMl5BanBnXkFtZTcwMjMxNTM4Nw@@.
       _V1_UX75_CR0,0,75,109_AL_.jpg',
       role: 'Maria Hill' },
     { name: 'Anthony Mackie',
       image: '
       https://ia.media-imdb.com/images/M/MV5BMTk3NTM1MjE2M15BMl5BanBnXkFtZTcwNzc5OTI2Mg@@.
       _V1_UY109_CR5,0,75,109_AL_.jpg',
       role: 'Sam Wilson/Falcon' },
     { name: 'Hayley Atwell',
       image: '
       https://ia.media-imdb.com/images/M/MV5BMjQ1OTkyOTA3MV5BMl5BanBnXkFtZTgwNzQ4MzE5ODE@.
       _V1_UY109_CR3,0,75,109_AL_.jpg',
       role: 'Peggy Carter' },
     { name: 'Idris Elba',
       image: '
       https://ia.media-imdb.com/images/M/MV5BNzEzMTI2NjEyNF5BMl5BanBnXkFtZTcwNTA0OTE4OA@@.
       _V1_UX75_CR0,0,75,109_AL_.jpg',
       role: 'Heimdall' },
     { name: 'Linda Cardellini',
       image: '
       https://ia.media-imdb.com/images/M/MV5BMTQ2MDM4MTM2NF5BMl5BanBnXkFtZTgwMTM4MjYyMDE@.
       _V1_UY109_CR2,0,75,109_AL_.jpg',
       role: 'Laura Barton' },
     { name: 'Stellan Skarsgård',
       image: '
       https://ia.media-imdb.com/images/M/MV5BMTg4NDUzOTY0N15BMl5BanBnXkFtZTYwNjYxODE0._V1_UX75_CR0,0,
       75,109_AL_.jpg',
       role: 'Erik Selvig' },
     { name: 'Claudia Kim',
       image: '
       https://ia.media-imdb.com/images/M/MV5BMTcyMzgxNTM4N15BMl5BanBnXkFtZTgwMjY1ODk4MzE@.
       _V1_UX75_CR0,0,75,109_AL_.jpg',
       role: 'Dr. Helen Cho' },
     { name: 'Thomas Kretschmann',
       image: '
       https://ia.media-imdb.com/images/M/MV5BMTY1Njc5MzE1OF5BMl5BanBnXkFtZTcwMTc1NDM4Nw@@.
       _V1_UY109_CR0,0,75,109_AL_.jpg',
       role: 'Strucker' } ] }

```
<h2>SIMPLESEARCH</h2>

```javascript
simpleSearch('flash').then((data)=>{
    console.log(data)
})
```
output:
```
{
   "v":1,
   "q":"flash",
   "d":[
      {
         "l":"The Flash",
         "id":"tt3107288",
         "s":"Grant Gustin, Candice Patton",
         "y":2014,
         "q":"TV series",
         "vt":19,
         "i":[
            
            "https://ia.media-imdb.
            com/images/M/MV5BZTQzNmEwZTMtZGNkNC00YjQ5LThhYzMtZTBhNzUzODI5ZjRjXkEyXkFqcGdeQXVyMjM5NzU3O
            TM@._V1_.jpg",
            1080,
            1350
         ],
         "v":[
            {
               "l":"Comic-Con Trailer",
               "id":"vi523352345",
               "s":"2:01",
               "i":[
                  
                  "https://ia.media-imdb.
                  com/images/M/MV5BNDE4OWI3OTktYTU5ZS00NjE1LThjZGUtMmNlZmNhNzJlYTZkXkEyXkFqcGdeQXVyMTk
                  xNjUyNQ@@._V1_.jpg",
                  1280,
                  720
               ]
            },
            {
               "l":"Extended Season 3 Trailer",
               "id":"vi2912597529",
               "s":"1:00",
               "i":[
                  
                  "https://ia.media-imdb.
                  com/images/M/MV5BMTU3NjE5MjExMV5BMl5BanBnXkFtZTgwMDMzMDUxMDI@._V1_.jpg",
                  
                  1280,
                  720
               ]
            },
            {
               "l":"Season 3 Trailer From Comic-Con",
               "id":"vi1006679833",
               "s":"2:12",
               "i":[
                  
                  "https://ia.media-imdb.
                  com/images/M/MV5BMTU1MTkxNjU5MV5BMl5BanBnXkFtZTgwNTQ3NjI1OTE@._V1_.jpg",
                  
                  1280,
                  720
               ]
            }
         ]
      },
      {
         "l":"Flash Gordon",
         "id":"tt0080745",
         "s":"Sam J. Jones, Melody Anderson",
         "y":1980,
         "q":"feature",
         "i":[
            
            "https://ia.media-imdb.
            com/images/M/MV5BN2Y4ZDBjMjEtZWQ0OS00NzYyLTg0M2ItMmUzYTEwN2RmMGVlXkEyXkFqcGdeQXVyMjgyOTI1O
            DY@._V1_.jpg",
            1944,
            2988
         ]
      },
      {
         "l":"The Flash",
         "id":"tt0098798",
         "s":"John Wesley Shipp, Amanda Pays",
         "y":1990,
         "q":"TV series",
         "i":[
            
            "https://ia.media-imdb.com/images/M/MV5BMjAzOTkzNzk4OV5BMl5BanBnXkFtZTgwNzc0MzUzMzE@._V1_.
            jpg",
            
            500,
            375
         ]
      },
      {
         "l":"Untitled The Flash Film",
         "id":"tt0439572",
         "s":"Gal Gadot, Ezra Miller",
         "y":2020,
         "q":"feature"
      },
      {
         "l":"Ricki and the Flash",
         "id":"tt3623726",
         "s":"Meryl Streep, Kevin Kline",
         "y":2015,
         "q":"feature",
         "i":[
            
            "https://ia.media-imdb.com/images/M/MV5BMTY1NzIxNzkzM15BMl5BanBnXkFtZTgwMzAzNjIzNjE@._V1_.
            jpg",
            
            1382,
            2048
         ]
      },
      {
         "l":"Flash",
         "id":"tt0136199",
         "s":"Lucas Black, Brian Kerwin",
         "y":1997,
         "q":"TV episode",
         "i":[
            
            "https://ia.media-imdb.com/images/M/MV5BMTkwNzY4Mzg5N15BMl5BanBnXkFtZTcwNzE4MzEyMQ@@._V1_.
            jpg",
            
            286,
            475
         ]
      },
      {
         "l":"Lego DC Comics Super Heroes: The Flash",
         "id":"tt7877382",
         "s":"James Arnold Taylor, Kate Micucci",
         "y":2018,
         "q":"video",
         "i":[
            
            "https://ia.media-imdb.
            com/images/M/MV5BODY5NjI2OTEtODI2ZC00MjJhLTk5MTEtNmM5MzlmNTUwNzEwXkEyXkFqcGdeQXVyNTM3MDMyM
            DQ@._V1_.jpg",
            375,
            500
         ]
      },
      {
         "l":"Flash Gordon",
         "id":"tt0959086",
         "s":"Eric Johnson, Gina Holden",
         "y":2007,
         "q":"TV series",
         "i":[
            
            "https://ia.media-imdb.com/images/M/MV5BMTY2Njc1MTgyNV5BMl5BanBnXkFtZTcwODYwNTI1MQ@@._V1_.
            jpg",
            
            429,
            600
         ]
      }
   ]
}
```
<h3>GETTRENDING</h3>

```javascript
const {getTrending}=require('imdb-scrapper')
getTrending(7).then((data)=>{
  console.log(data)
})
```
```
{ trending:
   [ { name: 'A Quiet Place',
       poster: 'https://ia.media-imdb.com/images/M/MV5BMjI0MDMzNTQ0M15BMl5BanBnXkFtZTgwMTM5NzM3NDM@._V1_QL50.jpg',
       id: 'tt6644200' },
     { name: 'Avengers: Infinity War',
       poster: 'https://ia.media-imdb.com/images/M/MV5BMjMxNjY2MDU1OV5BMl5BanBnXkFtZTgwNzY1MTUwNTM@._V1_QL50.jpg',
       id: 'tt4154756' },
     { name: 'Ready Player One',
       poster: 'https://ia.media-imdb.com/images/M/MV5BY2JiYTNmZTctYTQ1OC00YjU4LWEwMjYtZjkwY2Y5MDI0OTU3XkEyXkFqc
       GdeQXVyNTI4MzE4MDU@._V1_QL50.jpg',
       id: 'tt1677720' },
     { name: 'Rampage',
       poster: 'https://ia.media-imdb.com/images/M/MV5BNDA1NjA3ODU3OV5BMl5BanBnXkFtZTgwOTg3MTIwNTM@._V1_QL50.jpg',
       id: 'tt2231461' },
     { name: 'The Meg',
       poster: 'https://ia.media-imdb.com/images/M/MV5BMTg1ODc2NDQzNF5BMl5BanBnXkFtZTgwOTY1OTUyNTM@._V1_QL50.jpg',
       id: 'tt4779682' },
     { name: 'Solo: A Star Wars Story',
       poster: 'https://ia.media-imdb.com/images/M/MV5BOTM2NTI3NTc3Nl5BMl5BanBnXkFtZTgwNzM1OTQyNTM@._V1_QL50.jpg',
       id: 'tt3778644' },
     { name: 'Black Panther',
       poster: 'https://ia.media-imdb.com/images/M/MV5BMTg1MTY2MjYzNV5BMl5BanBnXkFtZTgwMTc4NTMwNDI@._V1_QL50.jpg',
       id: 'tt1825683' } ] }

```
<h3>GETTRENDINGGENRE</h3>

```javascript
const {getTrendingGenre}=require('imdb-scrapper')
getTrendingGenre('comedy',7).then((data)=>{
  console.log(data)
})
```
```
{ trending:
   [ { name: 'A Series of Unfortunate Events',
       poster: 'https://ia.media-imdb.com/images/M/MV5BMjQ4OTg3ODkyMl5BMl5BanBnXkFtZTgwMjI0OTg5NDM@._V1_QL50.jpg',
       id: 'tt4834206' },
     { name: 'Blockers',
       poster: 'https://ia.media-imdb.com/images/M/MV5BMjE0ODIzNjkzMl5BMl5BanBnXkFtZTgwODQ3MzU4NDM@._V1_QL50.jpg',
       id: 'tt2531344' },
     { name: 'Suits',
       poster: 'https://ia.media-imdb.com/images/M/MV5BMTk1MjYzOTU2Nl5BMl5BanBnXkFtZTgwMzAxMTg5MTE@._V1_QL50.jpg',
       id: 'tt1632701' },
     { name: 'Jumanji: Welcome to the Jungle',
       poster: 'https://ia.media-imdb.com/images/M/MV5BODQ0NDhjYWItYTMxZi00NTk2LWIzNDEtOWZiYWYxZjc2MTgxXkEyXkFqc
       GdeQXVyMTQxNzMzNDI@._V1_QL50.jpg',
       id: 'tt2283362' },
     { name: 'Isle of Dogs',
       poster: 'https://ia.media-imdb.com/images/M/MV5BMTYyOTUwNjAxM15BMl5BanBnXkFtZTgwODcyMzE0NDM@._V1_QL50.jpg',
       id: 'tt5104604' },
     { name: 'Roseanne',
       poster: 'https://ia.media-imdb.com/images/M/MV5BMzQyZWExODMtZDFkOC00MGUxLTgxMmItZWVkMmYwYzgxY2ZlXkEyXkFqcGdeQXVyODQwNjgyMw@@._V1_QL50.jpg',
       id: 'tt0094540' },
     { name: 'Shameless',
       poster: 'https://ia.media-imdb.com/images/M/MV5BZjQ3ZjFkZmQtYjMwZS00ZWFkLTgyNGMtYTE1OTI5ZTAwNWI3XkEyXkFqcGdeQXVyNjc3OTUzNzM@._V1_QL50.jpg',
       id: 'tt1586680' } ] }

```