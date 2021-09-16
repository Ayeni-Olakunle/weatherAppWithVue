<template>
    <div id="app1">
        <div class="holdInfo">
            <div>
               <input type="text" v-model="inptes" class="input"><button @click="fetDB" class="button">{{butin}}</button>
                <div id="qwe">
                    <h3><span id="name"></span><span id="country"></span></h3>
                <p id="degree"></p>
                <h3 id="desc"></h3>    
                </div> 
            </div>
        </div>
        
    </div>
</template>

<script>
export default {
    name:"app1",
    data(){
        return{
            butin: "Get",
            inptes:""
        }
    },
    methods:{
        fetDB(){
            
            let inpteS = this.inptes;
            let key = "2f1af375771e27cd15ac6ea465735161";

            fetch(`https://api.openweathermap.org/data/2.5/weather?q=${inpteS},${inpteS},${inpteS}&appid=${key}`)
            .then(Response => Response.json())
            .then(data => {
                let conv = Math.round(parseFloat(data.main.temp)-268.15)
                document.getElementById("name").innerHTML = data.name
                document.getElementById("country").innerHTML = data.sys.country
                document.getElementById("degree").innerHTML = conv+"<sup>o</sup><span>C</span>"
                document.getElementById("desc").innerHTML = data.weather[0].main
            })
        }
    }   
}
</script>

<style scoped>
#app1{
    width: 100%;
    height: 500px;
}

.holdInfo{
    background-image: url("../assets/jonny-mckenna-4igCpD-Lnfg-unsplash.jpg");
    height: 500px;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    border-radius: 7px;
}
.input{
    width: 80%;
    padding: 10px 10px;
    font-size: 18px;
    border: none;
    outline: none;
    border-radius: 50px;
    margin: 20px;
}

.button{
    width: 10%;
    padding: 10px 10px;
    border: none;
    outline: none;
    border-radius: 50px;
    margin: 20px;
    font-size: medium;
    background-color: black;
    color: white;
    font-weight: 700;
    cursor: pointer;
    transition: .5s;
}

.button:hover{
    background-color:white;
    color: black;
}

#qwe{
    text-align: center;
    font-size: 30px;
    color: white;
}

#name{
    margin-right: 10px;
}

@media only screen and (max-width: 600px) {
  .input{
        width: 50%;
    }
    .button[data-v-c5276018] {
        width: 20%;
    }
}
</style>