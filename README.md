# GIT / GIT FLOW ALIASES
alias gs="git stash"
alias gsa="git stash apply"
alias gsl="git stash list"
alias gsc="git stash clear"

alias gft="git fetch --tags"
alias gpt="git push --tags"

# MERGES E CHECKOUTS ENTRE MASTER E DEVELOP
alias gcm="git checkout master"
alias gmm="git merge master"
alias gcd="git checkout develop"
alias gmd="git merge develop"

# FEATURES
gcf()  { git checkout feature/$1; }
gffs() { git flow feature start $1; }
gfff() { git flow feature finish -F $(git_flow_current_branch); }

# HOTFIXS
gch()  { git checkout hotfix/$1; }
gfhs() { git flow hotfix start $1; }
gfhf() { git fetch --tags; git pull origin master; git flow hotfix finish -F $(git_flow_current_branch); }

# RELEASE
gcr()  { git checkout release/$1;  }
gfrs() { git flow release start $1; }
gfrf() { git flow release finish -F $(git_flow_current_branch) -m "release $(git_flow_current_branch) implemented";}

# RESPONSÁVEL PARA OBTER O NOME DA BRANCH CORRENTE
git_flow_current_branch(){ git rev-parse --abbrev-ref HEAD | cut -d'/' -f 2; }

# RESPONSÁVEL PARA OBTER A ÚLTIMA TAG EXISTENTE
glt() {
	LAST_TAG=$(git for-each-ref --format="%(refname:short)" --sort=taggerdate refs/tags | tail -1 | git for-each-ref --format="%(refname:short)" --sort=taggerdate refs/tags | tail -1);
	echo $LAST_TAG | xargs echo -n | pbcopy;
	echo "LAST TAG: "$LAST_TAG;
}

# REMOVE A TAG E ATUALIZA NO REMOTO
gut (){
    git tag -d $1;
    git push origin :refs/tags/$1;
}
