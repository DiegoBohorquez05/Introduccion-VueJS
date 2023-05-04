<template>
  <!-- se puede manejar sintaxis de js sobre el template  -->
  <h1>Hola {{ name.toLowerCase() }}</h1>
  <h2>-----------------------------------------------------------------------</h2>

  <!-- manejar estilos desde una constante en el script -->
  <!-- es necesario en este caso usar las comillas invertidas  -->
  <h2 :style="`color: ${arrayColors[1]}`">Soy azul</h2>
  <h2>{{ arrayColors }}</h2>
  <h2>-----------------------------------------------------------------------</h2>

  <!-- usar un operador ternario para hacer un condicional  -->
  <h2>
    {{ activo ? 'Esta activo' : 'No esta activo' }}
  </h2>
  <h2>-----------------------------------------------------------------------</h2>

  <!-- hacer un if y un else -->
  <h2 v-if="activo === true">Estoy activo</h2>
  <h2 v-else-if="activo === false">Estoy inactivo</h2>
  <h2 v-else>estoy indeciso</h2>
  <h2>-----------------------------------------------------------------------</h2>

  <!-- No importa sobre que etiqueta se trabaje el v-if, lo importante es que se mantengan juntas, si se llega a colocar otra etiqueta intermedia va a danar el codigo -->
  <div v-if="activo === true">
  <h2>ESTOY ACTIVO</h2>
  </div>
  <div v-else-if="activo === false">
  <h2>ESTOY INACTIVO</h2>
  </div>
  <div v-else><h2>ESTOY CONFUNDIDO</h2></div>
  <h2>-----------------------------------------------------------------------</h2>

  <!-- el v-show hace la misma funcion que el v-if, pero este solo cambia el style de la etiqueta a display none, lo cual hace que no desaparezca el elemento del dom sino que solo se oculte  -->
  <!-- usar v-show unicamente cuando se necesiten hacer muchos cambios en la pagina, usar cuando se necesite ocultar o mostrar algo varias veces, sino es el caso usar preferiblemente v-if  -->
  <h2 v-show="activo">Estoy activo v-show</h2>
  <h2>-----------------------------------------------------------------------</h2>

  <!-- usar el v-for para recorrer arreglos u objetos, es importante que el primer parametro va a ser como se va a llamar para mostrar en el dom, despues va el in que es para ubicar de donde van a salir los datos y por ultimo va el nombre del arreglo u objeto -->
  <ul>
    <li v-for="fruta,index in frutas" :key="fruta">{{ index }} , {{ fruta }}</li>
    <!-- la key ayuda a vue a identificar los nodos, no va a hacer ningun cambio visual pero va a facilitar la carga y el mostrar los datos, es importante que en cada v-for que se haga poner una key unica para ese v-for dependiendo de los datos que se manejen  -->
  </ul>
  <h2>-----------------------------------------------------------------------</h2>
  <!-- recorrido de objetos con iteracion de datos  -->
  <ul>
    <li v-for="datos in datosFrutas" :key="datos.id">{{ datos.id }}, {{ datos.name }}, {{ datos.price }}, {{ datos.description }}</li> 
  </ul>
  <h2>-----------------------------------------------------------------------</h2>
  <!-- recorrido de un unico objeto  -->
  <ul>
    <li v-for="datos,propiedad in objetoFruta">{{ propiedad }}: {{ datos }}</li>
    <!-- en este caso el segundo argumento llama a la propiedad que tiene el nombre dentro del objeto, por eso se puede ver el campo del objeto, y ya como tercer argumento opcional esta el index que sigue haciendo su funcion de dar valores numericos empezando por 0 -->
  </ul>
  <h2>-----------------------------------------------------------------------</h2>
  <!-- trabajar un v-if dentro de un v-for de la siguiente manera, hay que hacerlo asi porque si se hace sobre la misma etiqueta marcara un error, ya que vue leera primera el v-if y despues el v-for, por ende el parametro que queremos evaluar en el v-if no existira porque no se a recorrido el objeto u arreglo  -->
  <ul>
    <li v-for="item in datosFrutasStock" :key="item.name">
    <span v-if="item.stock > 0">{{ item.name }} - {{ item.price }}, el stock es {{ item.stock }}</span>
    <span v-else>{{ item.name }}, el stock es 0</span>
    <!-- se puede obviamente usar todas las variables y complementos del v-if  -->
    </li>
  </ul>
  <h2>-----------------------------------------------------------------------</h2>
  <!-- para hacer interactividad con el usuario por ejemplo en el boton se usa el v-on, donde despues de los dos puntos se pone que esta esperando, y dentro de las comillas se pone el nombre de la funcion que se declarara en el script -->
  <button v-on:click="handleClick(texto)">Dar Click</button>
  <input type="text" id="texto">
  <span id="mostrar">texto</span>
  <!-- Aqui es un ejemplo sencillo de poner un texto en el input, dar click en el boton y mostrar eso que se escribio en consola y en el dom  -->
  <h2>-----------------------------------------------------------------------</h2>
  <!-- hacer un contador cada vez que haga un click  -->
  <button @click="increment">Aumentar</button>
</template>

<script setup>
  // declaracion de constantes
  const name= 'JavaScript'

  // declaracion de constantes de estilos
  const styleColor = 'color: blue'
  const arrayColors=["red","blue","gray"]

  // trabajo con booleanos
  const activo=true

  const frutas = ['banano','fresa','pera','manzana']

  const datosFrutas = [
    {
      id: 1,
      name: 'manzana',
      price: '300',
      description: 'color: red'
    },
    {
      id: 2,
      name: 'pera',
      price: '400',
      description: 'color: green'
    },
    {
      id: 3,
      name: 'banana',
      price: '700',
      description: 'color: yellow'
    }
  ]

  const objetoFruta = {
      id: 1,
      name: 'manzana',
      price: '300',
      description: 'color: red'
    }

    const datosFrutasStock = [
    {
      id: 1,
      name: 'manzana',
      price: '300',
      description: 'color: red',
      stock: 0
    },
    {
      id: 2,
      name: 'pera',
      price: '400',
      description: 'color: green',
      stock: 10
    },
    {
      id: 3,
      name: 'banana',
      price: '700',
      description: 'color: yellow',
      stock: 20
    }
  ]

  // funcion para mostrar un texto que se escribio en un input
  const handleClick=(message)=>{
    const texto = document.getElementById('texto').value
    const mostrar = document.getElementById('mostrar')
    mostrar.innerHTML=texto
    console.log(texto)
  }
  // funcion para hacer un contador sencillo
  let counter = 0
  const increment = () => {
    counter++
    console.log(counter);
  }
</script>


<!-- parte de estilos -->
<style>
h1{
  color: #f00;
}
</style>