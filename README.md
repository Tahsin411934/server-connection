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
        if work with json :
        const tourist = require('./tourist.json');


        // MIDDLEWARE

        app.use(cors());
        app.use(express.json());


        const { MongoClient, ServerApiVersion, ObjectId } = require('mongodb');
    const uri = "mongodb+srv://Phones:ub5kntIhpTeqkJ3l@cluster0.2vutuar.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0";

    // Create a MongoClient with a MongoClientOptions object to set the Stable API version
    const client = new MongoClient(uri, {
        serverApi: {
            version: ServerApiVersion.v1,
            strict: true,
            deprecationErrors: true,
        }
    });

    async function run() {
        try {
            const PhonesDB = client.db('Phones').collection('Phone');
            app.get("/phone", async (req, res) => {
                const find = PhonesDB.find();
                const result = await find.toArray();
                res.send(result)
            });

        app.get('/phone/:id', async (req, res) => {
            const id = req.params.id;
            const quary = { _id: new ObjectId(id) }
            const options = {
                projection: { brand: 0, color:0 },
            };
            const result = await PhonesDB.findOne(quary,options)
            res.send(result)
        });



        app.post("/touristSpot",async(req,res)=>{
            const touristSpot= req.body;
            const result= await touristSpots.insertOne(touristSpot)
            res.send(result)
        })

        app.delete("/touristSpots/:id", async (req, res) => {
            const id = req.params.id;
            const query = { _id: new ObjectId(id) };
            const result = await touristSpots.deleteOne(query);
            res.send(result)
        })

      app.put("/touristSpots/:id",async (req, res) => {
        const id = req.params.id;
        const tourist_Spot= req.body;
        console.log(id,tourist_Spot)
        const filter = { _id: new ObjectId(id) };
        const options = {upset: true};
        const updateSpot = {
          $set: {
            country_name: tourist_Spot.country_name,
            tourists_spot_name: tourist_Spot.tourists_spot_name,
            location: tourist_Spot.location,
            average_cost: tourist_Spot.average_cost,
            seasonality: tourist_Spot.seasonality,
            travel_time: tourist_Spot.travel_time,
            total_visitors_per_year: tourist_Spot.total_visitors_per_year,
            image: tourist_Spot.image,
            short_description: tourist_Spot.short_description,
          }
        }
        const result = await touristSpots.updateOne(filter,updateSpot,options);
        res.send(result)
    })




        console.log("Pinged your deployment. You successfully connected to MongoDB!");
    } finally {


    }
    }
    run().catch(console.dir);


        app.get("/", (req,res)=>{
            res.send('server is running');
        })

        app.listen(port, ()=>
            console.log('running port is ' , port )
        )

## client site: post:

        fetch('https://tourism-management-website-server-beta.vercel.app/touristSpot', {
            method: "POST",
            headers: {
                'content-type': 'application/json'
            },
            body: JSON.stringify(data)
            })
            .then(res => res.json())
            .then(data => console.log(data))

       ## delete:
            fetch(`https://tourism-management-website-server-beta.vercel.app/touristSpots/${_id}`, {
                    method: 'DELETE',
                })
                .then(res => res.json())
                .then(data =>console.log(delete)
                )


            Update:

                fetch(`https://tourism-management-website-server-beta.vercel.app/touristSpots/${updateSpot._id}`, {
                method: "PUT",
                headers: {
                    'content-type':'application/json'
                },
                body: JSON.stringify(data)
                })
                .then(res=>res.json())
                .then(responseData => {
                if (responseData.error) {
                    // If there is an error, show SweetAlert2 error message
                    Swal.fire({
                    title: 'Error!',
                    text: responseData.error,
                    icon: 'error',
                    confirmButtonText: 'Ok'
                    });
                } else {
                    // If successful, show success message
                    Swal.fire({
                    title: 'Success!',
                    text: 'Tourist spot Updated successfully',
                    icon: 'success',
                    confirmButtonText: 'Ok'
                    });
                }
        })
