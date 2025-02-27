# ProgIIIG1-Act02-Samuel_Zuleta-Miguel_Gallego-Santiago_Giraldo







# Reglas

nodos_conectados(X, Nodos, Costo) :- conexion_entre(X, Nodos, Costo).

tiene_aristas(X):- conexion_entre(X, _, _).

costo_de(X, Y, Costo):-conexion_entre(X, Y, C1).

costo_de(X, Y, Costo):- conexion_entre(X, Z, C1), costo_de(Z, Y, C2), Costo is C1+C2.

posible_viajar(X, Y):- conexion_entre(X, Y, _).

posible_viajar(X, Y):- conexion_entre(X, Z, _), posible_viajar(Z,Y).

