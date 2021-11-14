body{
	font-family: 'Open Sans',sans-serif;
	background-color:black;
}
#container{
	width: 1000px;
	height: 550px;
	margin: 20px auto;	
}
#calculator{
	width: 320px;
	height: 520px;
    background-color: #eaedef;
    margin: 0 auto;
    top: 20px;
    position: relative;
    border-radius: 5px;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0.2), 0 6px 20px 0 rgba(0,0,0,0.19);
}
#result{
    height: 120px;
}
#history{
    text-align: right;
    height: 20px;
    margin: 0 20px;
    padding-top: 20px;
    font-size: 15px;
    color: #919191;
}
#output{
    text-align: right;
    height: 60px;
    margin: 10px 20px;
    font-size: 30px;
    
    function getHistory(){
    return document.getElementById("history-value").innerText;
}
function printHistory(num){
    document.getElementById("history-value").innerText=num;
}
function getOutput(){
    return document.getElementById("output-values").innerText;
}
function printOutput(num){
    if(num==""){
    document.getElementById("output-values").innerText=num;
    }
    else{
        document.getElementById("output-values").innerText=getFormattedNumber(num);
    }
}
function getFormattedNumber(num){
    if(num=="-"){
        return "";
    }
    var n=Number(num);
    var value= n.toLocaleString("en");
    return value;
}
function reverseNumberFormat(num){
    return Number(num.replace(/,/g, ''));
}
var operator = document.getElementsByClassName("operator");
for( var i=0;i<operator.length;i++){
    operator[i].addEventListener('click',function(){
            if(this.id=="clear"){
                printHistory("");
                printOutput("");
            }
            else if(this.id=="backspace"){
                var
                output=reverseNumberFormat(getOutput()).toString();
                if(output){//if output has a value
                    output= output.substr(0,output.length-1);
                printOutput(output);
                }
            }
            else{
                var output = getOutput();
                var history = getHistory();
                if(output==""&&history!=""){
                    if(isNaN(history[history.length-1])){
                        history=history.substr(0,history.length-1);
                    }
                }
                if(output!="" || history!=""){
                    output= output==""?
                    output:reverseNumberFormat(output);
                    history=history+output;
                    if(this.id=="="){
                        var result= eval(history);
                        printOutput(result);
                        printHistory("");
                    }
                    else{
                        history=history+this.id;
                        printHistory(history);
                        printOutput("");
                    }
                }
            }
    });
}
var number = document.getElementsByClassName("number");
for(var i=0;i<number.length;i++){
    number[i].addEventListener('click',function(){
        var output=reverseNumberFormat(getOutput());
        if(output!=NaN){
            output=output+this.id;
            printOutput(output);
        }
    });
}

}
#keyboard{
    height: 400px;
}
.operator, .number, .empty{
    width: 50px;
    height: 50px;
    margin: 15px;
    float: left;
    border-radius: 50%;
    border-width: 0;
    font-size: 15px;
    font-weight: bold;

}
.number, .empty{
    background-color: #eaedef;
}
.operator{
    background-color:lightgrey;
}
.number, .operator{
    cursor: pointer;
}
.number:active, .operator:active{
    font-size: 13px;
}
.number:focus, .operator:focus, .empty:focus{
    outline: 0;
}
button:nth-child(4){
    font-size: 20px;
    background-color: #20b2aa;
}
button:nth-child(8){
    font-size: 20px;
    background-color: #ffa500;
}
button:nth-child(12){
    font-size: 20px;
    background-color: #f08080;
}
button:nth-child(16){
    font-size: 20px;
    background-color: #7d93e0;
}
button:nth-child(20){
    font-size: 20px;
    background-color: #9477af;
}
