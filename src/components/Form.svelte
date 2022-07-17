
<div class="main-index">
    <div class="form-div">
      <p>Tabs</p>
      <div class="nav">
        <nav id="tab-form">
          <div class="form-input">
            <div class="form-container">
                <label for="numTabs" class="numTabs">Num.Tabs</label>
                <input placeholder="1" type="text" id="numTabs" class="inputNum" on:change={editNum}/>
            </div>
            {#if  num == 0}
                <div class="error"> Deve haver ao menos uma aba</div>
            {/if}
            <hr />

          </div>
            <form class="data-input">
                {#each array as id, index}
                    <div class="form-input">
                        <div class="form-container">
                        <label for="titulo" class="titulo">Título</label>
                        <input type="text" id="titulo" class="inputTitulo" bind:value={titulos[index]}/>
                        </div>
                        {#if !titulos[index] && erro == true}
                            <div class="error"> É necessário informar o título da aba</div>
                        {/if}
                        <div class="form-container">
                        <label for="textAConteudo" class="label-conteudo">Conteúdo</label>
                        <textarea id="conteudo" class="textAConteudo" bind:value={conteudos[index]}></textarea>
                        </div>
                        {#if  !conteudos[index] && erro == true}
                            <div class="error" > É necessário informar o conteúdo da aba</div>
                        {/if}
                  </div>
                {/each}
                <div class="form-btn">
                  <input type="button" class="submit-btn" value="Salvar" on:click={cadastro}/>
                </div>
            </form>
        </nav>
      </div>
    </div>
    <div class="conteudo">
      <p>Conteúdo</p>
      <Tabs ids={titulosF} contents={contentsF}></Tabs>
    </div>
</div>

<script>

import Tabs from "./Tabs.svelte";

let num = 1;
let array = [];
let count = 0;
let erro = false;

let titulos = [];
let conteudos =[];
let titulosF = [];
let contentsF =[];

 function editNum(event) {
            num = event.target.value;
            let rows = [];
            let aux = parseInt(num)
            for (let i = 0; i < aux; i++) {
            rows.push(i);
            }
            array = rows;
        }

 function cadastro(){

        count = 0;

        for (let i = 0; i < num; i++) {
        if (!titulos[i]) {
            erro = true;
            count = count + 1;
        }
        if (!conteudos[i]) {
            erro = true;
            count = count + 1;
        }
        }

        if(count == 0){
            titulosF = titulos
            contentsF = conteudos
        }

}

</script>

<style>

div.main-index{
width: 100%;
display: flex;
flex-flow: row;
align-items: center;
justify-content: space-between;
}

div.form-div{
align-items: flex-start;
width: 100%;
margin: 5px;
margin-left: 20px;
margin-bottom: 20px;
margin-top: 20px;
padding: 10px;
box-shadow: 0 0 1em gray;
}

div.conteudo{
width: 100%;
margin: 50px;
padding: 10px;
box-shadow: 0 0 1em gray;
}

div.form-div p{
font-family:Arial, Helvetica, sans-serif ;
font-size: 25px;
font-weight: bold;
}


div.conteudo p{
font-family:Arial, Helvetica, sans-serif ;
font-size: 25px;
font-weight: bold;
}

.submit-btn{
background-color: rebeccapurple;
width: 100px;
color: #e8f0f2;
font-weight: bold;
border-radius: 10%;
padding: 10px;
font-size: 16px;
margin: 0 auto;
cursor: pointer;
transition: .5s;
align-items: flex-end;
margin-bottom: 10px;
}

.submit-btn:hover{
background-color: transparent;
color: #222;
}

div.form-btn {
text-align: right;
}

#tab-form{
width: 100%;
margin: 0 auto;
align-items: center;
}

.form-input{
    text-align: right;
    margin-bottom: 10px;
}

input{
padding: 5px 10px;
width: 500px;
border-color: rgb(184, 181, 181);
border-radius: 5px;
}

textarea{
padding: 5px 10px;
width: 500px;
border-color: rgb(184, 181, 181);
border-radius: 5px;
}

label{
margin-top: 0;
font-weight: bold;
margin-bottom: 5px;
color: #222;
padding: 5px 10px;
}

.label-conteudo{

vertical-align:top
}

hr{
text-align: right;
width: 94%;
margin-right: 0;
}

.error{
    margin-top: 0;
color: red;
margin-bottom: 7px;
}

.form-container{
    display: flex;
    align-items: center;
    justify-content: right;
    margin-bottom: 7px;
}


</style>