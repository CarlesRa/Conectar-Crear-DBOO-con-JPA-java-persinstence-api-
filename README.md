# Conectar a base de datos orientada a objetos con java

Fracción de codigo ejemplo para crear y utilizar una base de datos orientada a objetos en java mediante JPA (java persistence api).

```java
package com.carlesramos;

import com.carlesramos.personas.Persona;
import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;
import javax.persistence.Persistence;
import javax.persistence.Query;
import java.util.List;

public class Main {
    public static void main(String[] args) {

        Persona p;

        //creamos/assignamos el archivo .odb, donde se guardaran los objetos
        EntityManagerFactory emf = Persistence.createEntityManagerFactory("$objectdb/db/st.odb");

        //Creamos el EntityManager, para insertar, consultar, modificar la dataBase .odb
        EntityManager em = emf.createEntityManager();

        //Iniciamos la Transicion
        em.getTransaction().begin();

        //Creamos objetos de la clase Persona
        p = new Persona("manolo");

        //instanciamos un objeto persistente
        em.persist(p);
        p = new Persona("Juan");
        em.persist(p);
        p = new Persona("Paco");
        em.persist(p);
        p = new Persona("Maria");
        em.persist(p);

        //guardamos los cambios en la base de datos.
        em.getTransaction().commit();

        //ejecutamos unas consultas utilizando el EntityManager
        Query q1 = em.createQuery("SELECT p FROM Persona p");
        Query q2 = em.createQuery("SELECT name FROM Persona");

        //imprimimos los resultados
        List<Persona>resultados = q1.getResultList();
        for (Persona pAux : resultados){
            System.out.println(pAux.toString());
        }
        System.out.println(q2.getResultList());
    }
}
```
