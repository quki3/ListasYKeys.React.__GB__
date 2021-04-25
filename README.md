Listas y keys
Primero, vamos a revisar como transformas listas en Javascript.

Dado el código de abajo, usamos la función map() para tomar un array de numbers y duplicar sus valores. Asignamos el nuevo array devuelto por map() a la variable doubled y la mostramos:

const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);
console.log(doubled);

Renderizado de Múltiples Componentes
Puedes hacer colecciones de elementos e incluirlos en JSX usando llaves {}.
Debajo, recorreremos el array numbers usando la función map() de Javascript. Devolvemos un elemento <li> por cada ítem . Finalmente, asignamos el array de elementos resultante a listItems:

const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);
Incluimos entero el array listItems dentro de un elemento <ul>, y lo renderizamos al DOM:

ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);

Componente básico de lista
Usualmente renderizarías listas dentro de un componente.

Podemos refactorizar el ejemplo anterior en un componente que acepte un array de numbers e imprima una lista de elementos.

Cuando ejecutes este código, serás advertido que una key debería ser proporcionada para ítems de lista. Una “key” es un atributo especial string que debes incluir al crear listas de elementos. Vamos a discutir por qué esto es importante en la próxima sección.

Vamos a asignar una key a nuestra lista de ítems dentro de numbers.map() y arreglar el problema de la falta de key.
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);

Keys
Las keys ayudan a React a identificar que ítems han cambiado, son agregados, o son eliminados. Las keys deben ser dadas a los elementos dentro del array para darle a los elementos una identidad estable:

La mejor forma de elegir una key es usando un string que identifique únicamente a un elemento de la lista entre sus hermanos. Habitualmente vas a usar IDs de tus datos como key:

const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
Cuando no tengas IDs estables para renderizar, puedes usar el índice del ítem como una key como último recurso:

const todoItems = todos.map((todo, index) =>
  // Only do this if items have no stable IDs
  <li key={index}>
    {todo.text}
  </li>
);

Integrar map() en JSX
En los ejemplos de arriba declaramos una variable separada listItems y la incluimos en JSX:

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
JSX permite integrar cualquier expresión en llaves así que podemos alinear el resultado de map():

function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />
      )}
    </ul>
  );
}