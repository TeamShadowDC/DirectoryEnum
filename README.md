# DirectoryEnum

Script para poder enumerar muchos ficheros de un CTF, puedes hacer el mismo comando para todos los ficheros.

## Ejemplo de uso
```
enum file
```


## Codigo
```bash
#!/bin/bash

Author: Marc Hortelano

greenColour="\e[0;32m\033[1m"
grayColour="\e[0;37m\033[1m"
redColour="\e[0;31m\033[1m"
yellowColour="\e[0;33m\033[1m"
endColour="\033[0m\e[0m"

# Variables 
comand=$*

function ctrl_c(){

        echo -e "\n${grayColour}[!]${endColour}${redColour} Exiting...${endColour}"; sleep 1
        tput cnorm; exit 1
}

function main(){

  while IFS= read -r line; do
    echo -e "\n${grayColour}[*]${endColour} ${greenColour}$comand $line ; ${endColour}" 
    if [[ -d $line ]]; then 
      echo -e "${grayColour}[-]${endColour}${yellowColour} $line es un directorio${endColour}"
    else
      echo "$comand \"$line\""| bash 
    fi 
    echo -e "${grayColour}- - - - - - - - - - - - - - - - - - - - - -${endColour}"
  done < <(ls)
}

main

```

