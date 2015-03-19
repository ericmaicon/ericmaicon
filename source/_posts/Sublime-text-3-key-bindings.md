title: "Sublime text 3 key bindings"
date: 2015-02-16 22:57:51
categories:
- Sublime Text
tags:
- Sublime Text
---
![Sublime Text](/thumbnails/sublime.jpg)

It is so hard to find an IDE that works with all keybinds that you want to. I never get used to with eclipse, netbeans, PHPStorm and others IDE keybinds. When I started to use Sublime Text, I found a simple way to configure and customize it. So, here it goes my custom key bindings:

```javascript
/*
sublime.log_commands(True)
*/
[
  /*
  abre os arquivos
  */
  {
     "keys":["shift+command+r"], 
     "command": "show_overlay", 
     "args": {
        "overlay": "goto",
        "show_files": true
     }
  },

  /*
  maiúsculo/minúsculo
  */
  {
     "keys":["shift+command+x"],
     "command": "upper_case"
  },

  {
     "keys":["shift+command+j"],
     "command": "lower_case"
  },

  /*
  importar classes
  */
  {
     "keys":["shift+command+i"],
     "command": "find_use"
  },

  /*
  Definição da classe
   */
  {
     "keys":["f3"],
     "command": "goto_definition_scope"
  },

  /*
  pesquisa
  */
  {
     "keys":["command+f"],
     "command": "show_panel",
     "args": {
        "panel": "replace"
     }
  },

  
  {
     "keys":["command+t"],
     "command" : "run_multiple_commands",
      "args" : {
          "commands" : [
              {
                  "command" : "trim",
                  "context": "window"
              },
              {
                  "command" : "trim_edges",
                  "context": "window"
              }
          ]
      }
  },

  {
     "keys":["command+h"],
     "command": "find_in_folder",
     "args": {
        "dirs": [""]
     }
  },

  /*
  fechar pagina
  */
  {
     "keys":["command+w"],
     "command": "close"
  },

  /*
  vai para a linha
  */
  {
     "keys": ["command+g"],
     "command": "show_overlay", 
     "args": {
        "overlay": "goto", 
        "text": ":"
     }
  },

  /*
  lista de métodos
  */
  {
     "keys":["command+o"],
     "command": "show_overlay",
     "args": {
        "overlay": "goto", 
        "text": "@"
     }
  },

  /*início e fim da linha*/
  {
     "keys": ["option+left"], 
     "command": "move_to",
     "args": {
        "to": "hardbol"
     }
  },
  {
     "keys": ["option+right"], 
     "command": "move_to",
     "args": {
        "to": "hardeol"
     }
  },
  {
     "keys": ["option+shift+left"], 
     "command": "move_to",
     "args": {
        "to": "hardbol",
        "extend": true
     }
  },
  {
     "keys": ["option+shift+right"], 
     "command": "move_to",
     "args": {
        "to": "hardeol", 
        "extend": true
     }
  },

  /*início e fim da palavra*/
  {
     "keys": ["command+left"], 
     "command": "move_to",
     "args": {
        "to": "bol"
     }
  },
  {
     "keys": ["command+right"], 
     "command": "move_to",
     "args": {
        "to": "eol"
     }
  },
  {
     "keys": ["command+shift+left"], 
     "command": "move_to",
     "args": {
        "to": "bol",
        "extend": true
     }
  },
  {
     "keys": ["command+shift+right"], 
     "command": "move_to",
     "args": {
        "to": "eol", 
        "extend": true
     }
  },

  /*
  abas
  */
  {
     "keys": ["control+shift+tab"], 
     "command": "prev_view_in_stack" 
  },
  {
     "keys": ["control+tab"], 
     "command": "next_view_in_stack"
  },
  
  /*início e fim do documento*/
  {
    "keys": ["command+up"], 
    "command": "move_to", 
    "args": {
      "to": "bof"
    }
  },
  {
    "keys": ["command+down"], 
    "command": "move_to", 
    "args": {
      "to": "eof"
    }
  },

  /*
  deletar linhas
  */
  {
     "keys": ["command+d"], 
     "command": "run_macro_file", 
     "args": {
        "file": "Packages/Default/Delete Line.sublime-macro"
     }
  },

  /*
  comentários
  */
  { 
     "keys": ["shift+command+c"], 
     "command": "toggle_comment", 
     "args": { 
        "block": false 
     } 
  },
  { 
     "keys": ["shift+command+t"], 
     "command": "toggle_comment", 
     "args": { 
        "block": true 
     } 
  },

  /*snnipets*/
  {
     "keys": ["command+1"], 
     "command": "insert", 
     "args": {
        "characters": "<?php"
     }
  },

  {
     "keys": ["command+2"], 
     "command": "insert", 
     "args": {
        "characters": "<%= %>"
     }
  },

  {
     "keys": ["command+3"], 
     "command": "insert_snippet", 
     "args": {
        "name": "Packages/User/console_log.sublime-snippet"
     }
  },

  {
     "keys": ["command+4"], 
     "command": "insert_snippet", 
     "args": {
        "name": "Packages/User/var_dump.sublime-snippet"
     }
  }
]
```