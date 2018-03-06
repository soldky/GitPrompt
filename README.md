# Git Prompt

## Colors
- Red : Non tracked files
- Yellow : Non commit
- Purple : Conflict
- Green : All is good

```# PROMPT COLOURS
BLACK='\e[0;30m'      # Black - Regular
RED='\e[0;31m'        # Red
GREEN='\e[0;32m'      # Green
YELLOW='\e[0;33m'     # Yellow
BLUE='\e[0;34m'       # Blue
PURPLE='\e[0;35m'     # Purple
CYAN='\e[0;36m'       # Cyan
WHITE='\e[0;37m'      # White
BLACK_BOLD='\e[1;30m'   # Black - Bold
RED_BOLD='\e[1;31m'     # Red - Bold
GREEN_BOLD='\e[1;32m'   # Green - Bold
YELLOW_BOLD='\e[1;33m'  # Yellow - Bold
BLUE_BOLD='\e[1;34m'    # Blue - Bold
PURPLE_BOLD='\e[1;35m'  # Purple - Bold
CYAN_BOLD='\e[1;36m'    # Cyan - Bold
WHITE_BOLD='\e[1;37m'   # White - Bold
RESET='\e[0m'         # Text Reset
PROMPT=''

parse_git_branch() 
{
  local BRANCH=$(git symbolic-ref HEAD --short 2> /dev/null)
  if [ ! -z "$BRANCH" ]
  then
    echo -e "($BRANCH)"

  else
    echo -e "(-)"
  fi
}

set_color()
{
  local STATUS=$(git st 2> /dev/null)

  if [[ "$STATUS" =~  "Fichiers non suivis" || "$STATUS" =~ "Modifications qui ne seront pas validées" ]]
  then
    echo -e "${RED_BOLD}"


  elif [[ "$STATUS" =~ "Modifications qui seront validées" ]] 
  then
    echo -e "${YELLOW_BOLD}"


  elif [[ "$STATUS" =~ "rien à valider" ]]
  then
    echo -e "${GREEN_BOLD}"

  elif [[ "$STATUS" =~ "ont divergé" ]]
  then
    echo -e "${PURPLE_BOLD}"

  else
    echo -e "${WHITE_BOLD}"
  fi
}
export PS1="\n${WHITE_BOLD}\u : ${CYAN_BOLD}[\w] \$(set_color)\$(parse_git_branch) ${WHITE_BOLD}\n▸ ${RESET}" ```
