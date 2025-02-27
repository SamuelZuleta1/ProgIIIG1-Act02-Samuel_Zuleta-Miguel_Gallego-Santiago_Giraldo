# ProgIIIG1-Act02-Samuel_Zuleta-Miguel_Gallego-Santiago_Giraldo


# Hechos

conexion(vancouver, edmonton, 16).

conexion(vancouver, calgary, 13).

conexion(edmonton, saskatoon, 12).

conexion(saskatoon, winnipeg, 20).

conexion(saskatoon, calgary, 9).

conexion(calgary, regina, 14).

conexion(calgary, edmonton, 4).

conexion(regina, winnipeg, 4).

conexion(regina, saskatoon, 7).


# Reglas

# Verificar si hay conexión directa entre dos ciudades.

hay_conexion_directa(Ciudad1, Ciudad2) :- 

    conexion(Ciudad1, Ciudad2, _).

# Obtener todas las conexiones de una ciudad.

conexiones_de(Ciudad, ConexionesDesde, ConexionesHacia) :-

    findall([Ciudad, Destino, Costo], conexion(Ciudad, Destino, Costo), ConexionesDesde),
    
    findall([Origen, Ciudad, Costo], conexion(Origen, Ciudad, Costo), ConexionesHacia).

# Encontrar un camino entre dos ciudades (incluyendo intermedias).

camino(Inicio, Fin, Camino, Costo) :-

    camino(Inicio, Fin, [Inicio], Camino, 0, Costo).

camino(Fin, Fin, _, [Fin], Costo, Costo).

camino(Actual, Fin, Visitados, [Actual|Camino], CostoActual, CostoTotal) :-

    conexion(Actual, Siguiente, CostoArista),
    
    \+ member(Siguiente, Visitados),
    
    NuevoCosto is CostoActual + CostoArista,
    
    camino(Siguiente, Fin, [Siguiente|Visitados], Camino, NuevoCosto, CostoTotal).

# Determinar si un nodo tiene aristas (salientes o entrantes).

tiene_aristas(Nodo) :-

    conexion(Nodo, _, _).  % Nodo con al menos una arista saliente

tiene_aristas(Nodo) :-

    conexion(_, Nodo, _).  % Nodo con al menos una arista entrante

# Determinar el costo de viajar de X a Z pasando por Y.

costo_via(X, Y, Z, CostoTotal) :-

    conexion(X, Y, Costo1),
    
    conexion(Y, Z, Costo2),
    
    CostoTotal is Costo1 + Costo2.

# Verificar si es posible viajar de una ciudad a otra.

puede_viajar(Inicio, Fin, Camino, Costo) :-

    camino(Inicio, Fin, Camino, Costo).

# Determinar si existe un camino entre dos ciudades.

existe_camino(Inicio, Fin) :-

    puede_viajar(Inicio, Fin, _, _), !.
    
existe_camino(_, _) :- 

    false.

# Ejecución del programa

Query: 

hay_conexion_directa(NOMBRE CIUDAD 1, NOMBRE CIUDAD 2).

![image](https://github.com/user-attachments/assets/d567b13b-edf7-4d1b-8e45-a78659e25111)

Query:

conexiones_de(NOMBRE DE LA CiUDAD, ConexionesDesde, ConexionesHacia).

![image](https://github.com/user-attachments/assets/efedf123-4f00-4c9a-be28-9faefc601809)

Query:

camino(NOMBRE CIUDAD 1, NOMBRE CIUDAD 2, Camino, Costo)

![image](https://github.com/user-attachments/assets/a0c50d7e-f68f-4c91-94de-0d3cb88a30b2)

Si devuelve False, no hay camino entre esas dos ciudades.

Query:

tiene_aristas(Nodo)

![image](https://github.com/user-attachments/assets/45dfc733-7dcd-4282-bd9e-1ade7f9997d7)

![image](https://github.com/user-attachments/assets/6886e727-822f-4bbf-b3f2-913059362ae7)

Query:

costo_via(X, Y, Z, CostoTotal).

![image](https://github.com/user-attachments/assets/5b82eaf3-6dc3-4f96-9aa0-ea9f86b2683b)


Query:

puede_viajar(Inicio, Fin, Camino, Costo).

![image](https://github.com/user-attachments/assets/3e321c89-423c-4c22-928a-419317af2599)





