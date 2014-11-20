mysqlnodeorm
============

Basic ORM for mysql module in node js 
DEPENDENCIAS
Este modulo depende de la libreria mysql para nodejs
INSTALACION
descarga npm install mysql
git clone git@github.com:Ditmar/mysqlnodeorm.git
USO
var mysql=require("./db/mysql.js");
var query=mysql({
    host:"localhost",
            user:"root",
            password:"",
            database:"database"
});
query.get("tablename").execute(function(rows){
  console.log(rows);
});
query.get("tablename").where({"id":1}).execute(function(rows){
  console.log(rows);
});
query.get("tablename").where({id:1}).where_or({id:2}).orderby("-id").limit(4).execute(function(rows){
  console.log(rows);
});
//consultas anidadas


query.get("usuario").execute(function(rows){
    //ejemplo la fila 5
    rows[5].all(rows[5].mensajes_table);
    rows[5].all(rows[5].comentarios_table,function(row){
        console.log(rows[5].comentarios[0]);
        var data=rows[5].comentarios[0];
        data.all(data.otro_table,function(another){
            console.log(rows);
        })
    });
});
