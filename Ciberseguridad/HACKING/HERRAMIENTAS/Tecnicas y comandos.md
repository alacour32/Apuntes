En esta fase es en la cual debes aprovechar de los resultados anteriores obtenidos, con esos resultados podrás buscar posibles exploits o maneras de aprovecharte de ellos, como por ejemplo:

- **FTP -Fuerza-Bruta:
```

		- hydra -l admin -P passlist.txt ftp://192.168.0.1
		- hydra -L userlist.txt -P passlist.txt ftp://192.168.0.1
```

Nota: Después de encontrar lo que te solicitan podrías necesitar unshadow y john

- **Reverse-Shell

Si te basas en los resultados anteriores y te ayudas de Google o searchsploit necesitarás:

- **Nc
```

		- nc -nlvp 443

```
- **Metasploit
```

		- msfconsole

```
