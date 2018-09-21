var express = require('express');
var app = express();
var fs=require('fs');
var bodyparse=require('body-parser');
var urlencodedParser=bodyparse({extended:false});
app.use(express.urlencoded());
app.use(bodyparse.json());

fs.writeFile('text.txt','Datas are',function(err)
{
    if (err) throw err;
    console.log('file created');
})

app.post('/save',function(req,res)
{
    var val=[{id:req.body.id,
 name:req.body.name,
 phone:req.body.phone,
 email:req.body.email
    }]
    
    console.log('get successfully');
    fs.appendFile('text.txt',JSON.stringify(val) ,function(err)
{
    if (err) throw err;
    console.log('file write succrssfully');

})

res.send('datas are save successfully!');
console.log('page open');
})
app.get('/view',function(req,res){
    res.sendFile(__dirname + "/" +"text.txt");
})

//app.get('/view',function(res,req)
//{
  //  fs.readFile('text.txt',function(res,data){
    //res.send(data);
   //console.log('opened');
    //})
//})


var server = app.listen(8081, function () {
   var host = server.address().address
   var port = server.address().port
   
   console.log("Example app listening at http://%s:%s", host, port)
});
