<p align="center">
   <img src="https://camo.githubusercontent.com/ab4c3c731a174a63df861f7b118d6c8a6c52040a021a552628db877bd518fe84/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f72656163742d2532333230323332612e7376673f7374796c653d666f722d7468652d6261646765266c6f676f3d7265616374266c6f676f436f6c6f723d253233363144414642">
  <img src="https://camo.githubusercontent.com/18d07ed577dd8860b7d3000e4e17d5ac7a042c02cfdd7fcec19873e5340d25b4/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f6c75612d2532333243324437322e7376673f7374796c653d666f722d7468652d6261646765266c6f676f3d6c7561266c6f676f436f6c6f723d7768697465">
  <img src="https://camo.githubusercontent.com/7d7b100e379663ee40a20989e6c61737e6396c1dafc3a7c6d2ada8d4447eb0e4/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f6e6f64652e6a732d3644413535463f7374796c653d666f722d7468652d6261646765266c6f676f3d6e6f64652e6a73266c6f676f436f6c6f723d7768697465">
  <img src="https://camo.githubusercontent.com/5b148e7e2d5fdb541ea3cae400ea95884b75202ebe9846d996a20971602a8f01/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f46697265626173652d3033394245353f7374796c653d666f722d7468652d6261646765266c6f676f3d4669726562617365266c6f676f436f6c6f723d7768697465">
  
</p>
<div align="center">
   <img align="center" src="https://static.wikia.nocookie.net/minecraft/images/f/fe/GrassNew.png/revision/latest/scale-to-width-down/250?cb=20190903234415"> 
<h1 align="center">Minecraft Control Hub</h1>
</div>


Este é meu projeto mais ambicioso que criei, permite que você acesse e interaja com items em seu mundo do minecraft (tanto singleplayer como um servidor), a partir do seu computadour ou do seu celular,
de qualquer lugar que estiver. Pense como se fosse algo como uma Casa Inteligente, só que no Minecraft;
</br>
</br>

Este projeto é uma expressão direta da minha criatividade e habilidades, desde a concepção até a implementação. Cada linha de código, design e funcionalidade foram ideias originadas completamente por mim, sem influências externas de cursos, tutoriais ou vídeos. É uma realização pessoal e um reflexo do meu compromisso com a inovação e o aprendizado autodidata.


Este é o repositório principal do projeto, mas o projeto é separado em Front-end e Back-end, caso queira ver o repositório do back-end:
</br>
<p align="center">(Back-end feito com Node.js)</p>
Por isso, caso tenha alguma dúvida, pode se sentir avontade para me enviar mensagem a respeito desse projeto e como criei e pensei em tal parte do projeto</br>
<p align="center">
   <a href="https://br.linkedin.com/in/daniel-kondlatsch" target="_blank">
      <img src="https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn">
   </a>
   <a href="mailto:danielpettres@gmail.com">
      <img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Enviar E-mail">
   </a>
</p>
</p>

<h1>Como funciona?</h1>
<p>Bom, primeiramente devemos evidenciar as dependências para que este projeto funcione.
</br>
Começando com a integração do Minecraft com a vida real, para conseguirmos fazer o Minecraft se conectar, interagir, enviar e receber (métodos GET e POST), nós usamos a biblioteca de mods 
<a href="https://files.minecraftforge.net/net/minecraftforge/forge/" target="_blank">Forge</a>, e apenas um mod(add-on) no Minecraft:
<a href="https://tweaked.cc/" target="_blank">CC:Tweaked </a>
</p>
</br>
<p>
   Explicando brevemente o que é o CC:Tweaked, ele é um mod que permite executar ações dentro do Minecraft usando a linguagem de programação Lua, substituindo métodos convencionais do próprio Minecraft, então ao invés de usar uma alavanca para acionar um sinal de restone, você pode simplesmente criar um programa em Lua que envie ou ative um sinal de redstone para tal lado/faceta do bloco.
</br>
</br>
Mas aqui resolvi elevar o nível da utilização deste mod: </br>
É colocado um computador do CC:Tweaked, embaixo de um baú, e neste computador, eu criei apenas um programa em Lua, que realiza o método POST para minha API que criei configurada para receber estes dados e formatá-los assim que receber.</br>
</br>

Por exemplo, no vídeo abaixo pode se ver um baú com 2 itens diferentes, e logo abaixo, nosso computador que executa o código reponsável por enviar
o dado dos itens contidos dentro do baú para nosso servidor.
</br>









https://github.com/dankwx/minecraft-irl-interaction/assets/63110149/977728db-1947-44cd-854f-f04a2fd05c40



E após o computador executar o programa, nosso baú aparece no nosso projeto:
![image](https://github.com/dankwx/minecraft-irl-interaction/assets/63110149/6ef4c922-c479-4cbc-9532-8c4b531a637e)





O programa realiza o seguinte: Verifica se existe um baú acima dele, se sim, lê todos itens e quantidades destes items e os envia em formato JSON para a API, esta API recebe os dados e os formata para que o front possa consumir e não haja necessidade de formatação de dados por parte do front, oque reduziria o desempenho. </br>
<details>
  <summary><strong>Código em Lua</strong></summary>
  
  <pre><code>
local url = "http://localhost:3001/baus"
local chest = peripheral.wrap("top")
local items = chest.list()
local data = {
  id = "baumine5",
  nome = "bau3",
  itens = {}
}
for slot, item in pairs(items) do
  table.insert(data.itens, {nome = item.name, quantidade = item.count})
end
local headers = {
  ["Content-Type"] = "application/json"
}
local response = http.post(url, textutils.serialiseJSON(data), headers)


  </code></pre>
  
</details>

E na nossa página principal, todos baús são exibidos e podemos ver os itens dentro deles um por um, como também podemos ver todos itens de todos baús.
Vale ressaltar que todos baús mostram os itens em ordem de maior quantidade para menor.








https://github.com/dankwx/minecraft-irl-interaction/assets/63110149/ddfbafd0-accb-41b2-aeac-2ab62a151964


</br>
Assim finalizo essa explicação sobre meu projeto. Já tenho planos para novas funções como interação com objetos (portas etc), que irei implantar em breve.





</p>


