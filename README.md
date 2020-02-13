# Taller de iniciación a ToneJS

Hace poco he ayudado a montar el <a href="https://zen.coderdojo.com/dojos/es/madrid/carabanchel-madrid-biblioteca-luis-rosales">CoderDojo de Carabanchel</a>, que es un club de programación donde niños y niñas de entre 7 y 17 años aprenden a programar ayudados por mentores. Nos reunimos los sábados por la tarde, y yo intento ir siempre que puedo con mis dos hijas. Además,  a veces preparo talleres. Al principio preparé un <a href="https://www.asanzdiego.com/2019/11/recursos-de-mi-taller-iniciacion-al-creative-coding-con-p5js-en-el-commitconf.html">taller de p5js, que es una librería de JavaScript para crear arte interactivo en el navegador</a> que gustó bastante, y ahora he preparado un taller de <a href="https://tonejs.github.io/">ToneJS una librería JavaScript para crear música interactiva en el navegador</a>. Este último taller está muy relacionado con un artículo que escribí hace justo un año en dónde explicaba <a href="https://www.asanzdiego.com/2019/02/programando-la-musica-de-star-wars-con-gibber.html">cómo programar la música de Star Wars con Gibber</a>.

Tenéis todo el código  y las librerías que necesitáis en un <a href="https://github.com/asanzdiego/taller-tonejs">repositorio de mi GitHub</a>.

Este es el código más básico para crear un botón que al pulsarlo haga sonar una nota, en este caso un DO, en el navegador:

<pre style="background: #f0f0f0; border: 1px dashed #CCCCCC;">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;ToneJS - 01 una nota&lt;/title&gt;
    &lt;script src="../lib/Tone.js"&gt;&lt;/script&gt;
  &lt;/head&gt;

  &lt;body&gt;
    &lt;button id="do"&gt;UNA NOTA&lt;/button&gt;
  &lt;/body&gt;

  &lt;script type="text/javascript"&gt;
    const synth = new Tone.Synth().toMaster();
    Tone.Transport.start();

    document.querySelector("#do")
      .addEventListener("click", async () =&gt; {
        synth.triggerAttackRelease("C4", "4n");
    });
  &lt;/script&gt;
&lt;/html&gt;</pre>

Puedes [abrir el ejemplo 01 directamente](https://asanzdiego.github.io/taller-tonejs/ejemplos/01-una-nota.html) o
ver el resultado a continuación (pulsa el botón para probar):

<div class="separator" style="clear: both; text-align: center;">
<iframe frameborder="1" height="50" src="https://asanzdiego.github.io/taller-tonejs/ejemplos/01-una-nota.html" width="140"></iframe></div>
En este punto hay que remarcar que las notas se ponen en el estilo anglosajón:

<ul>
<li>DO=C</li>
<li>RE=D</li>
<li>MI=E</li>
<li>FA=F</li>
<li>SOL=G</li>
<li>LA=A</li>
<li>SI=B</li>
</ul>

El número que sigue a la nota hace referencia a la octava (ya sea esta más grave o más aguda).

A continuación, parte del código para hacer una especie de piano con botones:

<pre style="background: #f0f0f0; border: 1px dashed #CCCCCC;">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;ToneJS - 02 varias notas&lt;/title&gt;
    &lt;script src="../lib/Tone.js"&gt;&lt;/script&gt;
  &lt;/head&gt;

  &lt;body&gt;
    &lt;button id="do"&gt;DO&lt;/button&gt;
    &lt;button id="re"&gt;RE&lt;/button&gt;
    ...
  &lt;/body&gt;

  &lt;script type="text/javascript"&gt;
    const synth = new Tone.Synth().toMaster();
    Tone.Transport.start();

    document.querySelector("#do")
      .addEventListener("click", async () =&gt; {
        synth.triggerAttackRelease("C4", "4n");
    });

    document.querySelector("#re")
      .addEventListener("click", async () =&gt; {
        synth.triggerAttackRelease("D4", "4n");
    });

    ...
  &lt;/script&gt;
&lt;/html&gt;</pre>

El resultado es el siguiente (pulsa los botones para probar) 

<div class="separator" style="clear: both; text-align: center;">
<iframe frameborder="1" height="50" src="https://asanzdiego.github.io/taller-tonejs/ejemplos/02-varias-notas.html" width="460"></iframe></div>
A continuación mostramos el código para que suene una escala:


<pre style="background: #f0f0f0; border: 1px dashed #CCCCCC;">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;ToneJS - 03 escala&lt;/title&gt;
    &lt;script src="../lib/Tone.js"&gt;&lt;/script&gt;
  &lt;/head&gt;

  &lt;body&gt;
    &lt;button id="escala"&gt;ESCALA&lt;/button&gt;
  &lt;/body&gt;

  &lt;script type="text/javascript"&gt;
    const synth = new Tone.Synth().toMaster();
    Tone.Transport.start();

    document.querySelector("#escala")
      .addEventListener("click", async () =&gt; {
        synth.triggerAttackRelease("C4", "8n", 1);
        synth.triggerAttackRelease("D4", "8n", 2);
        synth.triggerAttackRelease("E4", "8n", 3);
        synth.triggerAttackRelease("F4", "8n", 4);
        synth.triggerAttackRelease("G4", "8n", 5);
        synth.triggerAttackRelease("A4", "8n", 6);
        synth.triggerAttackRelease("B4", "8n", 7);
        synth.triggerAttackRelease("C5", "8n", 8);
    });
  &lt;/script&gt;
&lt;/html&gt;</pre>
El resultado es el siguiente (pulsa el botón para probar):

<div class="separator" style="clear: both; text-align: center;">
<iframe frameborder="1" height="50" src="https://asanzdiego.github.io/taller-tonejs/ejemplos/03-escala.html" width="140"></iframe></div>
Ahora hacemos algo un poco más elaborado utilizamos 2 arrays: uno para las notas y otro para las duraciones de las notas.


Aquí hay que remarcar que para los tiempos hay que tener en cuenta que:

<ul>
<li>1n hace referencia a una redonda (4 tiempos)</li>
<li>2n hace referencia a una blanca (2 tiempos)</li>
<li>4n hace referencia a una negra (1 tiempo)</li>
<li>8n hace referencia a una corchea (0,5 tiempos)</li>
<li>16n hace referencia a una semicorchea (0,25 tiempos)</li>
</ul>
Teniendo en cuenta esto, a continuación el código para hacer una escala con diferentes tiempos:


<pre style="background: #f0f0f0; border: 1px dashed #CCCCCC;">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;ToneJS - 04 notas&lt;/title&gt;
    &lt;script src="../lib/Tone.js"&gt;&lt;/script&gt;
    &lt;script src="../lib/Rhythm.js"&gt;&lt;/script&gt;
  &lt;/head&gt;

  &lt;body&gt;
    &lt;button id="notas"&gt;NOTAS&lt;/button&gt;
  &lt;/body&gt;

  &lt;script type="text/javascript"&gt;
    var synth = new Tone.Synth().toMaster();

    document.querySelector("#notas").addEventListener("click", async () =&gt; {

      var notas = [
        "C4","D4","E4","F4","G4","A4","B4","C5"];
      var duraciones = [
        "2n","4n","8n","16n","16n","8n","4n","2n"];

      var cancion = Rhythm.mergeDurationsAndPitch(duraciones, notas);

      var part = new Tone.Part(function(time, value){
        console.log(value.note + " " + value.duration);
        synth.triggerAttackRelease(value.note, value.duration, time);
      }, cancion );
      
      part.start(0);
      Tone.Transport.start();
    });
  &lt;/script&gt;
&lt;/html&gt;</pre>
El resultado es el siguiente (pulsa el botón para probar):

<div class="separator" style="clear: both; text-align: center;">
<iframe frameborder="1" height="50" src="https://asanzdiego.github.io/taller-tonejs/ejemplos/04-notas.html" width="140"></iframe></div>
Ahora vamos a coger una partitura sencilla, la del cumpleaños feliz:

<div class="separator" style="clear: both; text-align: center;">
<a href="https://1.bp.blogspot.com/-CdZsiQ2sju0/XjdOzZZLeiI/AAAAAAAADis/d4jEpfPBGZ498iqwVqtTiOI00NQoMXA2gCLcBGAsYHQ/s1600/05-cumplea%25C3%25B1os.jpg" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" data-original-height="305" data-original-width="640" height="305" src="https://1.bp.blogspot.com/-CdZsiQ2sju0/XjdOzZZLeiI/AAAAAAAADis/d4jEpfPBGZ498iqwVqtTiOI00NQoMXA2gCLcBGAsYHQ/s640/05-cumplea%25C3%25B1os.jpg" width="640" /></a></div>

Y la codificamos con ToneJS:


<pre style="background: #f0f0f0; border: 1px dashed #CCCCCC;">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;ToneJS - 05 cumpleaños feliz&lt;/title&gt;
    &lt;script src="../lib/Tone.js"&gt;&lt;/script&gt;
    &lt;script src="../lib/Rhythm.js"&gt;&lt;/script&gt;
  &lt;/head&gt;

  &lt;body&gt;
    &lt;button id="notas"&gt;CUMPLEAÑOS FELIZ&lt;/button&gt;
  &lt;/body&gt;

  &lt;script type="text/javascript"&gt;
    var synth = new Tone.Synth().toMaster();

    document.querySelector("#notas").addEventListener("click", async () =&gt; {

      var notas = [
        "C4", "C4", 
        "D4", "C4", "F4", 
        "E4", "C4", "C4", 
        "D4", "C4", "G4",
        "F4", "C4", "C4",
        "C5", "A4", "F4",
        "E4", "D4", "Bb4", "Bb4",
        "A4", "F4", "G4",
        "F4"];
      var duraciones = [
        "8n", "8n", 
        "4n", "4n", "4n",
        "2n", "8n", "8n",
        "4n", "4n", "4n",
        "2n", "8n", "8n", 
        "4n", "4n", "4n", 
        "4n", "4n", "8n", "8n",
        "4n", "4n", "4n",
        "2n"];

      var cancion = Rhythm.mergeDurationsAndPitch(duraciones, notas);

      var part = new Tone.Part(function(time, value){
        console.log(time + " " + value.note + " " + value.duration);
        synth.triggerAttackRelease(value.note, value.duration, time);
      }, cancion );
      
      part.start(0);
      Tone.Transport.start();
    });
  &lt;/script&gt;
&lt;/html&gt;</pre>
El resultado es el siguiente (pulsa el botón para probar):

<div class="separator" style="clear: both; text-align: center;">
<iframe frameborder="1" height="50" src="https://asanzdiego.github.io/taller-tonejs/ejemplos/05-cumpleaños.html" width="200"></iframe></div>
Y para terminar, hacemos lo mismo con la partitura de Star Wars:

<div class="separator" style="clear: both; text-align: center;">
<a href="https://1.bp.blogspot.com/-b2-JEFqCaic/XjdP7mf_4MI/AAAAAAAADi4/aEFEbBVVc2wot6n5VcofqnGAaFLKVQqqgCLcBGAsYHQ/s1600/06-starwars.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" data-original-height="478" data-original-width="640" height="478" src="https://1.bp.blogspot.com/-b2-JEFqCaic/XjdP7mf_4MI/AAAAAAAADi4/aEFEbBVVc2wot6n5VcofqnGAaFLKVQqqgCLcBGAsYHQ/s640/06-starwars.png" width="640" /></a></div>

Aquí hay que tener en cuenta que los trisillos se codifican con una t, en vez de con una n (ejemplo 8t). Y para los puntillos hay que disminuuir su número (ejemplo 3n).


<pre style="background: #f0f0f0; border: 1px dashed #CCCCCC;">&lt;!DOCTYPE html&gt;
&lt;html&gt;
  &lt;head&gt;
    &lt;title&gt;ToneJS - 06 Star Wars&lt;/title&gt;
    &lt;script src="../lib/Tone.js"&gt;&lt;/script&gt;
    &lt;script src="../lib/Rhythm.js"&gt;&lt;/script&gt;
  &lt;/head&gt;

  &lt;body&gt;
    &lt;button id="notas"&gt;Star Wars&lt;/button&gt;
  &lt;/body&gt;

  &lt;script type="text/javascript"&gt;
    var synth = new Tone.Synth().toMaster();

    document.querySelector("#notas").addEventListener("click", async () =&gt; {

var notas = [
        "F3", "C4",
        "Bb3", "A3", "G3", "F4", "C4",
        "Bb3", "A3", "G3", "F4", "C4",
        "Bb3", "A3", "Bb3", "G3", "C3", "C3", "C3",
        "F3", "C4",
        "Bb3", "A3", "G3", "F4", "C4",
        "Bb3", "A3", "Bb3", "G3", "C3", "C3",
        "D3", "D3", "Bb3", "A3", "G3", "F3",
        "F3", "G3", "A3", "G3", "D3", "E3", "C3", "C3",
        "D3", "D3", "Bb3", "A3", "G3", "F3",
        "C4", "G3", "G3", "C3", "C3",
        "D3", "D3", "Bb3", "A3", "G3", "F3",
        "F3", "G3", "A3", "G3", "D3", "E3", "C4", "C4",
        "F4", "F3",
        "C4", "C3", "C3", "C3",
        "F3", "C4",
        "Bb3", "A3", "G3", "F4", "C4",
        "Bb3", "A3", "G3", "F4", "C4",
        "Bb3", "A3", "Bb3", "G3", "C3", "C3", "C3",
        "F3", "C4",
        "Bb3", "A3", "G3", "F4", "C4",
        "Bb3", "A3", "G3", "F4", "C4",
        "Bb3", "A3", "Bb3", "G3", "C3", "C3", "C3",
        "F4", "F4", "F4", "F4", "F4"];
      var duraciones = [
        "2n", "2n",
        "8t", "8t", "8t", "2n", "4n",
        "8t", "8t", "8t", "2n", "4n",
        "8t", "8t", "8t", "2n", "8t", "8t", "8t",
        "2n", "2n",
        "8t", "8t", "8t", "2n", "4n",
        "8t", "8t", "8t", "2n", "8n", "8n",
        "3n", "8n", "8n", "8n", "8n", "8n",
        "8t", "8t", "8t", "8n", "8n", "4n", "8n", "8n",
        "3n", "8n", "8n", "8n", "8n", "8n",
        "8n", "8n", "2n", "8n", "8n",
        "3n", "8n", "8n", "8n", "8n", "8n",
        "8t", "8t", "8t", "8n", "8n", "4n", "8n", "8n",
        "2n", "2n",
        "1n", "8t", "8t", "8t",
        "2n", "2n",
        "8t", "8t", "8t", "2n", "4n",
        "8t", "8t", "8t", "2n", "4n",
        "8t", "8t", "8t", "2n", "8t", "8t", "8t",
        "2n", "2n",
        "8t", "8t", "8t", "2n", "4n",
        "8t", "8t", "8t", "2n", "4n",
        "8t", "8t", "8t", "2n", "8t", "8t", "8t",
        "4n", "8t", "8t", "8t", "4n"];

      var cancion = Rhythm.mergeDurationsAndPitch(duraciones, notas);

      var part = new Tone.Part(function(time, value){
        console.log(time + " " + value.note + " " + value.duration);
        synth.triggerAttackRelease(value.note, value.duration, time);
      }, cancion );
      
      part.start(0);
      Tone.Transport.start();
    });
  &lt;/script&gt;
&lt;/html&gt;</pre>
El resultado es el siguiente (pulsa el botón para probar):

<div class="separator" style="clear: both; text-align: center;">
<iframe frameborder="1" height="50" src="https://asanzdiego.github.io/taller-tonejs/ejemplos/06-starwars.html" width="140"></iframe></div>
Espero os haya gustado ;-)

## Recursos

<https://tonejs.github.io/>

<https://www.guitarland.com/MusicTheoryWithToneJS/TonejsSetup.html>