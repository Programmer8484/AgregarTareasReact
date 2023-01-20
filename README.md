# AgregarTareasReact
App para agregar tareas, creada con React y es responsive.

/*App.js*/
import './App.css';
import Tarea from './componentes/tarea';
import ListaDeTareas from './componentes/listaDeTareas';

function App() {
  return (
    <div className="aplicacion_tareas">
      <div className="tareas_lista_principal">
        <h1>Mis tareas.</h1>
        <ListaDeTareas/>
        
      </div>
    </div>
  );
}

export default App;

/*App.css*/
*{
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

body, 
html{
  color: white;
  background-color: rgba(29, 29, 104, 0.986);
  font-family: Georgia, 'Times New Roman', Times, serif;
  font-size: larger;
  margin-top: 40px;
}

h1{
  color: black;
  font-size: 30px;
  font-family: 'Times New Roman', Times, serif;
  text-align: center;
  margin: 20px 0; /*20 superior e inferior, 0 izquierda y derecha.*/
}

.aplicacion_tareas{
  display: flex;
  flex-wrap: wrap; /*Para que los elementos no se ajusten a una sola línea, se acomodan hacia abajo*/
  align-items: center;
  justify-content: center;
}

/*Lista de tareas.*/
.tareas_lista_principal{
  width: 600px;
  min-height: 500px;
  background-color: gray;
  padding: 25px;
  margin: 10px;
  border-radius: 25px;
}

/*Responsive*/

@media(max-width: 700px) {
  body,
  html{
    background-color: blue;
  }
}

@media(max-width: 400px) {
  body,
  html{
    background-color: brown;
    margin-top: auto;
  }

  h1{
    font-size: 20px;
    font-family: 'Times New Roman', Times, serif;
    text-align: center;
    margin: 10px 0;
  }

  .aplicacion_tareas{
    display: flex;
    flex-wrap: wrap; 
    align-items: center;
    justify-content: center;
  }

  .tareas_lista_principal{
    width: 300px;
    min-height: 200px;
    background-color: gray;
    padding: 10px;
    margin: 5px;
    border-radius: 15px;
  }
}

/*Tarea.js*/
import React from 'react';
import '../estilos/tarea.css'; 
import { AiOutlineClose } from 'react-icons/ai';


function Tarea({ id, texto, completada, completarTarea, eliminarTarea }){
    return (
        <div className={completada ? 'tarea-contenedor completada' : 'tarea-contenedor' }>
            <div 
                className='tarea-texto'
                onClick={() => completarTarea(id)}>
                {texto}
            </div>
            <div 
                className='tarea-contenedor-iconos'
                onClick={() => eliminarTarea(id)}>
                <AiOutlineClose className='tarea-icono' />   
            </div>
        </div>
    );
};

export default Tarea;

/*Tarea.css*/
.tarea-contenedor{
  width: 500px;
  min-height: 65px;
  background-color: #1b1b32;
  margin: 5px 0;
  padding: 8px 15px 8px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-radius: 7px;
  border: ipx solid white;
  cursor: pointer;
}

/*Colores*/
.tarea-contenedor:nth-child(3n + 1) {
  background-color: #1b1b32;
}

.tarea-contenedor:nth-child(3n + 2) {
  background-color: #2a2a40;
}

.tarea-contenedor:nth-child(3n + 3) {
  background-color: #3b3b4f;
}

/*Texto*/
.tarea-texto{
  width: 100%;
  height: 100%;
  font-size: 20px;
  display: flex;
  align-items: center;
  overflow-wrap: aniwhere; /*Si el texto de la tarea es muy largo, el texto es cortado y sigue hacia abajo.*/
}

/*Icono*/
.tarea-icono{
  width: 25px;
  height: 25px;
  margin: 25px;
}

/*Tarea completada.*/
.tarea-contenedor.completada{
  background-color: blueviolet;
  text-decoration: line-through;
}

@media(max-width: 400px) {
  .tarea-contenedor{
    width: 200px;
    height: 40px;
    background-color: #1b1b32;
    margin: 5px 0;
    padding: 4px 7px 4px 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-radius: 4px;
    border: ipx solid white;
    cursor: pointer;
  }

  .tarea-texto{
    width: 100%;
    height: 100%;
    font-size: 15px;
    display: flex;
    align-items: center;
    overflow-wrap: aniwhere; 
  }

  .tarea-icono{
    width: 13px;
    height: 13px;
    margin: 13px;
  }
}

/*Formulario.js*/
import React, { useState } from 'react';
import '../estilos/formulario.css';
import { v4 as uuidv4 } from 'uuid';

function TareaFormulario (props) {

  const [input, setInput] = useState('');

  const manejarCambio = e => {
    setInput(e.target.value);  
  };

  const manejarEnvio = e => {
    e.preventDefault();
    

    const tareaNueva = {
      id: uuidv4(),
      texto: input,
      completada:false
    };
    props.onSubmit(tareaNueva);
  };

  return (
    <form 
      className='tarea-formulario'
      onSubmit={manejarEnvio}>
      <input
        className='tarea-input'
        type='text'
        placeholder='Escribe una tarea.'
        name='texto'
        onChange={manejarCambio}
      />
      <button className='tarea-boton'>
        Agregar tarea.
        </button>
    </form>
  );
};

export default TareaFormulario;

/*Formulario.css*/
/*Estructura principal.*/
.tarea-formulario{
  display: flex;
  flex-wrap: wrap;
  align-items: center; /*Horizontal.*/
  justify-content: center; /*Vertical.*/
}

/*Campo de texto.*/
.tarea-input{
  width: 350px;
  font-size: 18px;
  background-color: aliceblue;
  padding: 14px 32px 14px 16px;
  border-radius: 4px 0 0 4px;
  border: 2px solid greenyellow;
  outline: none;
}

/*Botón*/
.tarea-boton{
  padding: 16px;
  font-size: 18px;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  border: none;
  border-radius: 0 4px 4px 0;
  cursor: pointer;
  outline: none;
  background: goldenrod;
  color: azure;
  text-transform: capitalize; /*Inicio de la palabra en mayúscula.*/
}

@media(max-width: 400px) {
  .tarea-formulario{
    display: flex;
    flex: auto;
    align-items: center; 
    justify-content: center; 
  }

  .tarea-input{
    width: 100px;
    font-size: 13px;
    background-color: aliceblue;
    padding: 7px 16px 7px 8px;
    border-radius: 4px 0 0 4px;
    border: 2px solid greenyellow;
    outline: none;
  }

  .tarea-boton{
    height: 30px;
    padding: 8px;
    font-size: 12px;
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    border: none;
    border-radius: 0 4px 4px 0;
    cursor: pointer;
    outline: none;
    background: goldenrod;
    color: azure;
    text-transform: capitalize; /*Inicio de la palabra en mayúscula.*/
  }


}

/*ListaDeTareas.js*/
import React, {useState} from 'react';
import TareaFormulario from './formulario';
import '../estilos/listaDeTareas.css';
import Tarea from './tarea';

/*Fragmento: etiquetas vacías.*/
function ListaDeTareas() {

  const [tareas, setTareas] = useState([]);

  const agregarTareas = tarea => {
    if (tarea.texto.trim()) {
      tarea.texto = tarea.texto.trim(); /*Trim quita los espacios del principio o final de la cadena.*/
      const tareasActualizadas = [tarea, ...tareas];
      setTareas(tareasActualizadas);
    }
  };

  const eliminarTarea = id => {
    const tareasActualizadas = tareas.filter(tarea => tarea.id !==id);
    setTareas(tareasActualizadas);
  };

  const completarTarea = id => {
    const tareasActualizadas = tareas.map(tarea => {
      if (tarea.id === id) {
        tarea.completada = !tarea.completada;
      }
      return tarea;
    });
    setTareas(tareasActualizadas);
  };

  return(
    <>
      <TareaFormulario onSubmit = {agregarTareas} />
      <div className='tareas-lista-contenedor'>
        {
          tareas.map((tarea) =>
            <Tarea 
              key={tarea.id}
              id={tarea.id}
              texto = {tarea.texto}
              completada = {tarea.completada}
              completarTarea={completarTarea}
              eliminarTarea={eliminarTarea} />
          )
        }
      </div>
    </>
  );
};

export default ListaDeTareas;

/*ListaDeTareas.css*/
.tareas-lista-contenedor{
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 15px;
}

//Index.js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

/*Index.css*/
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, 'Courier New',
    monospace;
}

/*Json*/
{
  "name": "aplicacion_de_tareas",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^5.16.5",
    "@testing-library/react": "^13.4.0",
    "@testing-library/user-event": "^13.5.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-icons": "^4.7.1",
    "react-scripts": "5.0.1",
    "uuid": "^9.0.0",
    "web-vitals": "^2.1.4"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}

/*Json*/
{
  "name": "aplicacion_de_tareas",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^5.16.5",
    "@testing-library/react": "^13.4.0",
    "@testing-library/user-event": "^13.5.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-icons": "^4.7.1",
    "react-scripts": "5.0.1",
    "uuid": "^9.0.0",
    "web-vitals": "^2.1.4"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
