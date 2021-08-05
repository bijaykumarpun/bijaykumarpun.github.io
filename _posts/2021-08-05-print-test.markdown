<html>
    <head>
        <title>
     Welcome
        </title>
        <style>
    :root {
    --primary-color: #22254b;
    --secondary-color: #373b69;
    --bg-color: rgb(241, 241, 241);
    --color-heading: rgb(44, 44, 44);
    --color-body: rgb(102, 102, 102);
 }
  
  body{
      background-color: rebeccapurple;
      margin: 0;
      padding: 0;
  }

  .container-main{
      display: flex;
     flex-direction: row;
      background-color: var(--bg-color);
      height:100vh;
      width:100vw ;
      align-items: center;
      justify-content: space-evenly;
  }

  .container-item{
      border-radius: 3px;
      height: 400px;
    box-shadow:0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
      width: 88mm;
      background-color: white;

  

  }
  #table-container {
      display: flex;
justify-content: center;

      /* border: 1px solid red; */
      
  
  }
  #table{
    margin-top: 10px;
     /* border: 1px solid green; */
      width:90%;
  }
  th {
      color: var(--color-heading);
      text-align: start;
      padding: 0 0 4px 0;

  }
  td {
      color: var(--color-body);
      text-align: start;

  }

  tr {
    
      margin: 0 0 8px 0;
  }

  #table-end{
      text-align: end;
      color: var(--color-heading);
/* border: 1px solid green; */
  }


#logo-container{
    width: 100%;

    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

#line{
    height: 1px;
    background-color: rgb(202, 202, 202);
    width: 100%;
    
}

.bold {
    color: black

}
 

#print-option {
    display: grid;
    flex-direction: column;
    align-items: center;
    justify-content: center;


}
 </style>
    </head>
  
    <body>
        
<div class="container-main">
    <div id="printThis">

<div class="container-item">
<div id="logo-container">
 <figure>
    <img src="logo.png"  width="130px" />
<figcaption style="color: rgb(39, 39, 39);">
    RedBull Suppliers Inc.
</figcaption>
 </figure>
<div id="line"></div>
</div >
    <div id="table-container">
        <table id="table">
           <tr>
            <th>Sn</th>
            <th>Particular</th>
            <th>Price</th>
            </tr>
            <tr>
            <td>1</td>
            <td>Party poppers</td>
            <td>$200</td>
            </tr>
            <tr>
                <td>2</td>
                <td>Birthday Cake</td>
                <td>$400</td>
                </tr>
                <tr>
                    <td>3</td>
                    <td>Birthday Hat</td>
                    <td>$300</td>
                    </tr>
                    <tr>
                        <td>4</td>
                        <td>Birthday Gift</td>
                        <td>$20</td>
                        </tr>
                        <tr>
                            <td>5</td>
                            <td>Ballon</td>
                            <td>$10</td>
                            </tr>
                        
                            <tr>
                                <td></td>
                                <td style="text-align: end; padding: 0 10px 0 0;" class="bold" >
                                Total
                                </td>
                                <td class="bold" >
                                    $880
                                </td>
                            </tr>

        </table>
      
    </div>
    <div id="endtext" style="margin-top:20px; width: 100%;
    font-size: 12px;
  
    display: flex; flex-direction: row; 
    justify-content: center;
    " >
***
    </div>
</div>
</div>

<div class="container-item" id="print-option">

<button onclick="printElem(document.getElementById('printThis'))" style="padding: 10px; width: 100px;">Print Bill</button>


</div>
</div>
</div>

        <script>
function printFunction(){
    console.log("Printing");

    if(document.getElementById("printThis")==null){
console.log("Element not found")
    }
printElem(printThis)
  
}

function printElem(elem)
{
    if(elem==null){
        console.log("Element missing")
    }else{
        console.log("Element found")
    }
    var mywindow = window.open('', 'PRINT', ('width=80mm'));

    mywindow.document.write('<html><head><link href="style.css" rel="stylesheet"/>');
    mywindow.document.write('</head><body >');
    // mywindow.document.write('<h1>' + document.title  + '</h1>');
    mywindow.document.write(elem.innerHTML);
    mywindow.document.write('</body></html>');

    mywindow.document.close(); // necessary for IE >= 10
    mywindow.focus(); // necessary for IE >= 10*/
    // document.onload =function() {
        mywindow.print();
        mywindow.close();
    // }


    return true;
}

        </script>
    </body>
</html>