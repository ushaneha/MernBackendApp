1.  create a new folder 'mernbackend' on your desktop
2.  open that folder in vs code
3.  open a cmd terminal
4.  Type 'npm init -y' in cmd
5.  You will see a that a 'package.json' file will be created
6.  install node and mongodb (also set env var for mongodb bin in path of sys variables)
    and also install 'mongodb compass' from 'https://www.mongodb.com/try/download/compass'
    and finally give 'npm install mongoose' in cmd to install mongoose
7.  Type 'npm i express' in cmd
8.  Now you can see a 'package-lock.json' file is created
9.  Type 'npm i hbs' in cmd
10. Now, type 'mkdir src' in cmd
11. type 'cd src' in cmd
12. type 'mkdir db' in cmd
13. type 'mkdir models' in cmd
14. type 'type nul > app.js' in cmd
15. Now, go to 'app.js' file and type the below code
    [
    const express = require("express");
    const app = express();
    const port = process.env.PORT || 3000;

        app.get("/", (req, res) => {
            res.send("welcome to web development training")
        });

        app.listen(port, () => {
            console.log(`server is running at port no ${port}`);
        })

    ]

16. Next, go to terminal and type 'cd..' to be back in project directory
17. Now, type 'node src/app.js' in cmd
18. You will be seeing 'server is running at port no 3000' as output in terminal
19. if your open any browser and type 'localhost:3000'
20. you should see 'welcome to web development training' displayed in webpage
21. go to cmd, and type 'npm i nodemon'
22. In the 'package.json' file, modify the "scripts:{}" by adding "dev" as shown below
    [
    "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev" : "nodemon src/app.js"
    },
    ]
23. Now, go to terminal, and type 'cls'
24. In the terminal, type 'npm run dev'
25. The output in the terminal is
    '[nodemon] starting `node src/app.js`'
26. In the 'db' folder, create a new file 'conn.js'
27. Open mongodb compass, you will see 'localhost:27017',
    we'll add it in the 'conn.js' file in the next step
28. Goto 'conn.js' file, and write the below code
    [
    const mongoose = require("mongoose");

        mongoose.connect("mongodb://localhost:27017/userRegistration", {
        }).then(() => {
            console.log(`connection successful`);
        }).catch((e) => {
            console.log(`connection failed`)
        })

    ]

29. Now, add this connection in 'app.js' file as shown below
    [
    require("./db/conn"); // add it just below const app = express();
    ]
30. Now, if you check the terminal, you will see
    'server is running at port no 3000' and
    'connection successful'
31. Now create a new folder 'public' in the project root folder 'mernbackend'
32. Inside this public folder, create a new file 'index.html'
33. Now, in this 'index.html' file, add the below line of code
    [
    <!DOCTYPE html>
    <html lang="en">
    <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MERN</title>
    </head>
    <body>
    <h1>MERN PROJECT</h1>
    </body>
    </html>
    ]
34. Goto 'app.js' file and add the below lines of code
    [
    const path = require("path");
    // add it below const express = require("express"); line of code

        console.log(path.join(__dirname, "../public")); // add it below const port = process.env.PORT || 3000;
        // use it once to check path in terminal and later on comment it output

        //while printing the above statement comment outthe below 2 lines of code and uncomment them later
        const static_path = path.join(__dirname, "../public");
        app.use(express.static(static_path));

    ]

35. Now, if you go to browser and reload the webpage,
    we should be seeing 'MERN PROJECT' as output
36. Now, let us add styling to our project, for that
    create a new folder 'css' inside 'public' folder
37. Inside this css folder, create a new file 'style.css'
38. Goto 'index.html' file, add the link of css in head section as shown below
    [
    <link rel="stylesheet" href="css/style.css">
    ]
39. Now, let us add a color to the header. Goto 'style.css' file and write the code below
    [
    h1{
    color: red;
    text-align: center;
    }
    ]
40. If we go back and check the output in the browser, you will see header will be in center and in red color
41. Now, all of this is static website. Let us make our website to be dynamic, so for that, let us delete 'index.html' file
42. Let us now create a new folder 'views' and
    inside that folder create a new file 'index.hbs'
43. In the 'app.js' file, add the below lines of code
    [
    app.set("view engine", "hbs")
    // add this line just below app.use(express.static(static_path)); line
    ]
44. Now in the same 'app.js' file, modify the 'app.get function' and keep the rest of the code as it is as shown below
    [
    app.get("/", (req, res) => {
    res.render("index")
    });
    ]
45. Now go back and check the output in the browser,
    you will see output is coming from 'index.hbs' template engine
46. In the 'views' folder, let's create a new file 'login.hbs'
47. Again in the same 'views' folder, let's create aother new file 'register.hbs'
48. Now that we are done creating all files needed for our app, let's rename the 'views' folder to be 'templates' folder
49. Inside the templates folder, let's now create the new folder as 'views' folder
50. Again Inside the 'templates' folder, let's create a new folder 'partials'
51. Now, move the all the exisiting 'hbs' files ('index.hbs','login.hbs','register.hbs') files inside 'views' folder
52. Inside the 'partials' folder, let's create a new file 'navbar.hbs'
53. In the 'navbar.hbs' file, let's add some code as shown below
    [
    <h1>navbar</h1>
    ]
54. To use this code inside the 'navbar.hbs' file, inside 'index.hbs' file, goto body section of 'index.hbs' file and add the below code as first line in body section
    [
    {{>navbar}}
    ]
55. Now, let's go to 'app.js' file and add the newly updated path of views as shown below
    [
    const template_path = path.join(**dirname, "../templates/views"); // Add it below 'const static_path = path.join(**dirname, "../public");' line

    ]

56. Now we have to let our application know about the updated template path.
57. So, in the same 'app.js' file, add the below line of code as shown below
    [
    app.set("views", template_path); // Add it below 'app.set("view engine", "hbs");' line

    ]

58. In the same 'app.js' file, now let us tell our express application that we are using 'hbs' template
59. For this, we need to add the below line of code in the 'app.js' file as shown below
    [
    const hbs = require("hbs"); // Add this line below 'const app = express();' line
    ]
60. In the same 'app.js' file, let us register our partials as shown below
    [
    hbs.registerPartials(partials_path); // Add this line below 'app.set("views", template_path);' line

    ]

61. Now let declare this 'partials_path' in the same 'app.js' file as shown below
    [
    const partials_path = path.join(__dirname, "../templates/partials"); // Add this line below 'const template_path = path.join(__dirname, "../templates/views");' this line
    ]
62. Now for reflecting changes of code modifications of 'hbs' files, we'll have to update the "dev" in 'package.json' file
    [
    "dev": "nodemon src/app.js -e js,hbs"
    ]
63. If the server is already running please restart it for applying above changes
64. Now, in the 'partials folder', let's create a new file 'header.hbs'
65. In the 'app.js' file, add the below line of code
    [
    app.get("/register", (req, res) => {
    res.render("register");
    });
            // add this method after this method [
            //        app.get("/", (req, res) => {
            //            res.render("index");
            //    });
            ]
    ]
66. Edit the code in the 'register.hbs' file as shown below
    [
    <!doctype html>
    <html lang="en">

        <head>
            {{>header}}
            <!-- Required meta tags -->
            <meta charset="utf-8">
            <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

            <!-- Bootstrap CSS -->
            <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css"
                integrity="sha384-xOolHFLEh07PJGoPkLv1IbcEPTNtaed2xpHsD9ESMhqIYd0nLMwNLD69Npy4HI+N" crossorigin="anonymous">

            <title>registration</title>
        </head>

        <body>
            /
            {{>navbar}}
                <form action="/register" method="post">
                <div class="form-group row">
                    <label for="inputname3" class="col-sm-2 col-form-label" name="firstname">First Name</label>
                    <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputname3">
                    </div>
                </div>
                <div class="form-group row">
                    <label for="inputEmail3" class="col-sm-2 col-form-label" name="email">Email</label>
                    <div class="col-sm-10">
                    <input type="email" class="form-control" id="inputEmail3">
                    </div>
                </div>
                <div class="form-group row">
                    <label for="inputphonenumber3" class="col-sm-2 col-form-label" name="phone">Phone</label>
                    <div class="col-sm-10">
                    <input type="text" minlength="10" maxlength="10"  class="form-control" id="inputphonenumber3">
                    </div>
                </div>
                <div class="form-group row">
                    <label for="inputPassword3" class="col-sm-2 col-form-label">Password</label>
                    <div class="col-sm-10">
                    <input type="password" class="form-control" id="inputPassword3" name="password">
                    </div>
                </div>
                <div class="form-check">
                <input class="form-check-input" type="radio" name="gender" id="exampleRadios1" value="option1" checked>
                <label class="form-check-label" for="exampleRadios1">
                    Male
                </label>
                </div>
                <div class="form-check">
                <input class="form-check-input" type="radio" name="gender" id="exampleRadios2" value="option2">
                <label class="form-check-label" for="exampleRadios2">
                    Female
                </label>
                </div>
                <div class="form-group row">
                    <label for="inputlastname3" class="col-sm-2 col-form-label" name="lasatname">Last Name</label>
                    <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputlastname3">
                    </div>
                </div>
                <div class="form-group">
                    <input type="text" name="age" placeholder="Enter Your Age *">
                </div>
                <div class="form-group">
                    <input type="password" name="" class="form-control" placeholder="Confirm Password *" />
                </div>
                <input type="submit" value="Register" class="btnRegister"   />
                </form>
            <!-- Optional JavaScript; choose one of the two! -->

            <!-- Option 1: jQuery and Bootstrap Bundle (includes Popper) -->
            <script src="https://cdn.jsdelivr.net/npm/jquery@3.5.1/dist/jquery.slim.min.js"
                integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj"
                crossorigin="anonymous"></script>
            <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/js/bootstrap.bundle.min.js"
                integrity="sha384-Fy6S3B9q64WdZWQUiU+q4/2Lc9npb8tCaSX9FK7E8HnRr0Jz8D6OP9dO5Vg3Q9ct"
                crossorigin="anonymous"></script>

            <!-- Option 2: Separate Popper and Bootstrap JS -->
            <!--
            <script src="https://cdn.jsdelivr.net/npm/jquery@3.5.1/dist/jquery.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
            <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
            <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/js/bootstrap.min.js" integrity="sha384-+sLIOodYLS7CIrQpBjl+C7nPvqq+FbNUBDunl/OZv93DB7Ln/533i8e/mZXLi/P+" crossorigin="anonymous"></script>
            -->
        </body>
        </html>

    ]

67. In the 'models' folder, let's create a new file 'registers.js' file
68. It's time to write code in this 'registers.js' file as shown below
    [
    const mongoose = require("mongoose");

            // We will define a schema(database) as shown below
            const employeeSchema = new mongoose.Schema({
                firstname: {
                    type:String,
                    required:true
                },
                lastname: {
                    type:String,
                    required:true
                },
                email: {
                    type:String,
                    required:true,
                    unique:true
                },
                gender: {
                    type:String,
                    required:true,
                },
                phone: {
                    type:Number,
                    required:true,
                    unique:true
                },
                age: {
                    type:Number,
                    required:true,
                },
                password: {
                    type:String,
                    required:true,
                },
                confirmpassword: {
                    type:String,
                    required:true,
                }
            })

            // Let us now create a collection
            // first create a model
            const Register = new mongoose.model("Register", employeeSchema);

            // Now let us export this model
            module.exports = Register;

    ]

69. Now, we have to get the models in the 'app.js' file
    [
    const Register = require("./models/registers");
    // Add this line below 'require("./db/conn");' this line
    ]
70. In the same 'app.js' file, let's add the post method as shown below
    [
    app.post("/register", async (req, res) => {
    try {
    const password = req.body.password;
    const cpassword = req.body.confirmpassword;

                    if(password === cpassword){
                        const registerEmployee = new Register({
                            firstname : req.body.firstname,
                            lastname  : req.body.lastname,
                            email     : req.body.email,
                            gender    : req.body.gender,
                            phone     : req.body.phone,
                            age       : req.body.age,
                            password  : password,
                            confirmpassword: cpassword
                        })
                        const registered = await registerEmployee.save();
                        res.status(201).render("index");
                    }else{
                        res.send("passwords are not matching")
                    }
                } catch (error) {
                    res.status(400).send(error);
                }
            });
        // Add the above code just before 'app.listen()' method

    ]

71. Again in 'app.js' file, add the below two lines of code
    [
    app.use(express.json());
    app.use(express.urlencoded({extended:false}));

        // Add this line below 'const partials_path = path.join(__dirname, "../templates/partials");' this line

    ]

72. Open compass , connect db, keep it running dont close it
73. please check all files for code as the last step
74. Thank you
