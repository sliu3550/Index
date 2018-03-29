<html>
<head>
<title> Open Parking and Camera Violations </title>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
* {
   box-sizing: border-box;
}

body {
 margin: 0;
}

/* Style the header */
.header {
   font-family:"Arial";
   text-shadow:gray 2px 2px 2px;
   background-color: #f1f1f1;
   padding: 20px;
   text-align: center;
}

/* Style the top navigation bar */
.topnav {
   overflow: hidden;
   background-color: #333;
}

/* Style the topnav links */
.topnav a {
   float: left;
   display: block;
   color: #f2f2f2;
   text-align: center;
   padding: 14px 16px;
   text-decoration: none;
}

/* Change color on hover */
.topnav a:hover {
   background-color: #ddd;
   color: black;
}

/* Create three equal columns that floats next to each other */
.column {
   float: left;
   width: 33.33%;
   padding: 15px;
}

/* Clear floats after the columns */
.row:after {
   content: "";
   display: table;
   clear: both;
}

/* Responsive layout - makes the three columns stack on top of each other instead of next to each other */
@media screen and (max-width:600px) {
   .column {
       width: 100%;
   }
}


  .card{
      width:350px;
      padding:10px;
      margin:10px;
      display:inline-block;
      border-radius:10px;
      box-shadow:black 5px 5px 5px;
  }
  h2{
      font-family: "Arial";
      font-size:27px;
  }
  p1{
      font-style: "Arial";
      font-size: 23px;
}

  img{
      width:90%;
      margin:5px;
      border-radius:10px;
      box-shadow:black 5px 5px 5px;
  }

</style>
</head>


<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/mustache.js/2.3.0/mustache.min.js"></script>
<script type="text/template" id="template">
  <div class="card">
      <h1 class="normal"> {{plate}}</h1>
     <p class="small"> {{state}} </P>
     <p class+"small"> {{issue_date}} </p>
     <marquee> {{violation}} </marquee>
 </div>
</script>
<script>
  var data;
 function search(){
     $.getJSON("https://data.cityofnewyork.us/resource/uvbq-3m68.json",function(results){
         data=results
     })
 }
 function displaydata(){
     var build="";
     var output=document.getElementById("output");
     var tmp = document.getElementById("template").innerHTML;
     var information=document.getElementById("info");
     for(var index=0;index<data.length;index++){
         if(data[index].plate.toLowerCase().indexOf(information.value.toLowerCase()) != -1 ){
         build+= Mustache.render(tmp,data[index]);
          }
     }
     output.innerHTML= build
 }
</script>
<body onload="search()">
<div class="header">
 <h1>Open Parking and Camera Violations</h1>
</div>
<div class="topnav">
 <a href="https://data.cityofnewyork.us/resource/uvbq-3m68.json">Link</a>
</div>
<input type = "text" id="info" placeholder="Enter Plate #">
<button onclick="displaydata()">Search</button>
<div class="row">
   <div class="column">
       <h2>Description</h2>
       <p1>This dataset contains Open Parking and Camera Violations issued by the City of New York. Updates will be applied to this data set on the following schedule. New or open
       tickets will be updated weekly (Sunday) Tickets satisfied will be updated daily (Tuesday through Sunday). You can search the information using the plate number. </p1>
   </div>
   <div class="column">
       <h2>Image Of JsonOnlineEditor</h2>
       <img src="Capture1.png" alt="JsonEditor">
   </div>
   <div class="column">
       <h2>Image 2</h2>
        <img src="Capture2.png" alt="JsonEditor">
    </div>
</div>
 <div id="output">
 </div>
</body>
</html>


