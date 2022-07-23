<template>
  <div class="hello">
    <div>
      <svg t="1658493015029" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="1412" width="64" height="64"><path d="M128 832a32 32 0 0 0-32 32v128a32 32 0 0 0 64 0v-128a32 32 0 0 0-32-32zM896 640a32 32 0 0 0 32-32V288a32 32 0 0 0-64 0v320a32 32 0 0 0 32 32zM896 192a32 32 0 0 0 32-32V32a32 32 0 0 0-64 0v128a32 32 0 0 0 32 32zM992 800a96 96 0 0 0-185.6-33.92 263.04 263.04 0 0 1-215.04-154.56l-100.16-224a327.36 327.36 0 0 0-272.64-192A96 96 0 0 0 160 133.76V32a32 32 0 0 0-64 0v101.76a96 96 0 0 0 0 180.48V736a32 32 0 0 0 64 0V314.24a96 96 0 0 0 57.6-56.32 263.04 263.04 0 0 1 215.04 154.56l100.16 224a327.36 327.36 0 0 0 272.64 192A96 96 0 0 0 864 890.24V992a32 32 0 0 0 64 0v-101.76A96 96 0 0 0 992 800zM128 256a32 32 0 1 1 32-32 32 32 0 0 1-32 32z m768 576a32 32 0 1 1 32-32 32 32 0 0 1-32 32z" fill="#38004D" p-id="1413"></path><path d="M128 896a96 96 0 1 1 96-96 96 96 0 0 1-96 96z m0-128a32 32 0 1 0 32 32 32 32 0 0 0-32-32zM896 320a96 96 0 1 1 96-96 96 96 0 0 1-96 96z m0-128a32 32 0 1 0 32 32 32 32 0 0 0-32-32z" fill="#9F85EC" p-id="1414"></path><path d="M192 832a32 32 0 0 1 0-64 263.68 263.68 0 0 0 240.64-156.48l100.16-224A327.68 327.68 0 0 1 832 192a32 32 0 0 1 0 64 263.68 263.68 0 0 0-240.64 156.48l-100.16 224A327.68 327.68 0 0 1 192 832z" fill="#9F85EC" p-id="1415"></path></svg>
    </div>
     <el-tooltip class="item" effect="dark" content="暂不支持中文" placement="top-start">
     
        <el-input v-model="str" placeholder="要加密部分" class="input"></el-input>
     
    </el-tooltip>
    <div class="button">
        <el-button @click="transform">加密</el-button>
        <el-button @click="transform1">解码</el-button>
    </div>
        

      <div class="text">转码的后内容</div>

      <div class="www">
        <div class="OUT">
        <div class="output">
          {{content}}
        </div>
      </div> 
      </div>
      

  </div>


</template>

<script>
import { computed } from 'vue';
export default {
  name: 'HelloWorld',

  data:function(){
    return{
      str: "",
      base64: "",
      content: '',

      decoded:""
    }
  },

  // mounted(){
  //   this.base(this.str)
  // },

  // computed:{

  //   password: function(){

  //     this.base(this.str)
  //     return `${this.base64}`
  //   }

  // },
 methods: {
  transform() {
    this.base(this.str);
    this.content = this.base64;
  },

  transform1(){
    this.decode(this.str);
    this.content = this.decoded;
  },

base:function (str){
    let map = new Map([["0","A"],["1","B"],["2","C"],["3","D"],["4","E"],["5","F"],["6","G"],["7","H"],["8","I"],["9","J"],["10","K"],["11","L"],["12","M"],["13","N"],["14","O"],
    ["15","P"],["16","Q"],["17","R"],["18","S"],["19","T"],["20","U"],["21","V"],["22","W"],["23","X"],["24","Y"],["25","Z"],["26","a"],["27","b"],["28","c"],
    ["29","d"],["30","e"],["31","f"],["32","g"],["33","h"],["34","i"],["35","j"],["36","k"],["37","l"],["38","m"],["39","n"],["40","o"],["41","p"],["42","q"],["43","r"],["44","s"],
    ["45","t"],["46","u"],["47","v"],["48","w"],["49","x"],["50","y"],["51","z"],["52","0"],["53","1"],["54","2"],["55","3"],["56","4"],["57","5"],["58","6"],["59","7"],["60","8"],
    ["61","9"],["62","+"],["63","/"]]);

    const len = str.length;
    let s = "";
    for(let i = 0 ; i<len; i++)
    {
        let sl = str[i].charCodeAt().toString(2);
        for(let j = 0; j<8-sl.length; j++)
        {
            sl = "0" +sl;
        }
        s+=sl;
    }
    if(s.length%6 !== 0)
    {
        const num = s.length%6;
        for(let i = 0; i<6-num; i++)
        {
            s += "0";
        }
        
    }
    let array = [];
    let newlen = parseInt((str.length*8)/6);
    let base = "";
    if(str.length % 3 ===0)
    {
        for(let i = 0 ; i<newlen; i++)
        {
           
            array.push(s.slice(i*6,(i+1)*6));
            array[i] =parseInt(Number(array[i]),2).toString();
        }
        for(let i = 0 ; i<newlen; i++)
        {
            base += map.get(array[i])
        }
    }
    else
    {
        for(let i = 0 ; i<=newlen; i++)
        {
           
            array.push(s.slice(i*6,(i+1)*6));
            array[i] =parseInt(Number(array[i]),2).toString();
        }
        for(let i = 0 ; i<=newlen; i++)
        {
            base += map.get(array[i]);
        }

        for(let i = 0; i<3 - str.length%3; i++)
        {
            base += "=";
        }
    }
    this.base64 = base;
  },

  decode:function(str){

    let map = new Map([["A",0],["B",1],["C",2],["D",3],["E",4],["F",5],["G",6],["H",7],["I",8],["J",9],["K",10],["L",11],["M",12],["N",13],["O",14],
    ["P",15],["Q",16],["R",17],["S",18],["T",19],["U",20],["V",21],["W",22],["X",23],["Y",24],["Z",25],["a",26],["b",27],["c",28],
    ["d",29],["e",30],["f",31],["g",32],["h",33],["i",34],["j",35],["k",36],["l",37],["m",38],["n",39],["o",40],["p",41],["q",42],["r",43],["s",44],
    ["t",45],["u",46],["v",47],["w",48],["x",49],["y",50],["z",51],["0",52],["1",53],["2",54],["3",55],["4",56],["5",57],["6",58],["7",59],["8",60],
    ["9",61],["+",62],["/",63]]);
    let i = str.length-1;
    while(str[i] === "=")      //去除 = 号
    {
        str = str.slice(0,i)
        i --;
    }
    const j = str.length % 4;
    const len = str.length;
    let newstr = "";
    if( j === 3)
    {
        for(let i = 0; i<len; i++)
        {
            let temp = map.get(str[i]).toString(2); 
                while(temp.length<6)
                {
                    temp = 0 + temp;
                }
                newstr+=temp;
        }
        newstr = newstr.slice(0,newstr.length-2)
   
    }
    else if(j === 2)
    {
        for(let i = 0; i<len; i++)
        { 
            let temp = map.get(str[i]).toString(2); 
            while(temp.length<6)
            {
                temp = 0 + temp;
            }
            newstr+=temp;
        }
        newstr = newstr.slice(0,newstr.length-4)
    }
    else
    {
        for(let i = 0; i<len; i++)
        { 
            let temp = map.get(str[i]).toString(2); 
            while(temp.length<6)
            {
                temp = 0 + temp;
            }
            newstr+=temp;
        }
    }
    let array = [];
    for(let newlen = 0; newlen < newstr.length/8; newlen++)
    {
        array.push(newstr.slice(newlen*8,(newlen+1)*8));
    }
    // console.log(array);
    let laststr = "";
    for(let newlen = 0; newlen < array.length; newlen++)
    {
        laststr += String.fromCharCode(parseInt(array[newlen],2))
    }
    
    this.decoded = laststr;

  }

}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.button{
  margin-top: 15px;
}
.input{
  width: 800px;
  margin-top: 50px;
}

.www{
  display: flex;
  justify-content: center;
}
#OUT{
  
  display: flex;
  justify-content: center;

}
.output{

  width: 600px;
  height: 200px;
  margin-top: 20px;
  border: 1px solid black;
  border-radius: 6px;
}

.text{
  margin-top: 30px;
  text-align: center;
}
</style>
