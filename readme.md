# Ejercicios de DIP, ISP, SRP
## Ejercicio 1 

**DIP:** No se está cumpliendo con DIP, ya que la clases Analizador de datos y Base de Datos dependen de cosas concretas, en lugar de depender de abstracciones. El Analizador de datos debería tener una abstacción entre él y la base de datos, evitando así la dependencia directa.
Lo mismo sucede en el método CumpleCondición, el parámetro recibido es concreto (DatebaseObject) y podría ser una abstracción.

**ISP:** Ninguna de las clases implementa Interfaces o hereda de otros tipos, por lo que no existe dependecia a otros tipos en los clientes y no se genera ningun conflicto.

**SRP:** Existe más de una razón por la que la clase podría cambiar, por lo que no se está cumpliendo con el SRP. Por ejemplo un cambio en el DatabaseObject, llevaría a cambiar la lógica implementada en BaseDeDatos y el analizador de datos debería ser modificado cada vez que se quiera agregar una condición a validar.


## Ejercicio 2 y 3
```cs
abstract class DataObject{
    public string Descripcion { get;}
}
class DataBaseObject : DataObject
{
}

//Base de datos.
class BaseDeDatos : IDataStructure
{
    public DataObject ObtenerDato(string clave)
    {
        //Devuelve el dato correspondiente a la clave
    }
    public void GrabarDato(string clave, DataObject dato)
    {
        //Graba el dato en la base de datos, bajo la clave dada
    }
    public String[] ListarClaves()
    {
        //Devuelve un String[] con todas las claves
    }
    public String[] ListarDescripcionDatos()
    {
        //Devuelve un String[] con la descripción de todas los 
        //datos almacenados en  la base
    }
    public DataObject[] ListarDatos()
    {
//Devuelve un DataObject[] con todos los datos almacenados en la base
    }
}
interface IDataStructure
{
    DataObject ObtenerDato(string clave);
    void GrabarDato(string clave, DataObject dato);
    String[] ListarClaves();
    String[] ListarDescripcionDatos();
    DataObject[] ListarDatos();
}
class AnalizadorDatos
{
    private IDataStructure baseDatos{get; set;};
    public void Analizar()
    {
        foreach (DataObject DObj in baseDatos.ListarDatos())
        {
            if (CumpleCondicion(DObj, ICondition))
            {
                ICondition.PrintMessage();
            }
        }
    }
    public bool Cumplecondicion(DataObject Dobj, ICondition condition)
    {
    return condition.Check(Dobj);
    }
}

interface ICondition {
    bool Check(DataObject obj);
    void PrintMessage();
}
```
