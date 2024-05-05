## install
         npm init -y

         npm i express cors mongodb dotenv



## create index.js file

## packsage.json < scripts < "start" : "node index.js"

## index.js file:

        const express = require('express');
        const cors = require('cors');
        const app = express();
        const port = process.env.PORT || 5000;


        // MIDDLEWARE

        app.use(cors());
        app.use(express.json());

        app.get("/", (req,res)=>{
            res.send('server is running');
        })

        app.listen(port, ()=>
            console.log('running port is ' , port )
        )

##