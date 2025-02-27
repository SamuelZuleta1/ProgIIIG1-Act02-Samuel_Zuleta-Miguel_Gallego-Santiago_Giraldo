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


