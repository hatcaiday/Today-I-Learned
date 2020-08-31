When we use github we usually spend a lot of time to typing each command. To increase performance, I will show you some function as below:

**Fetch PR and checkout**
```
gcp() {
  git fetch sun pull/$1/head:pullrequest/$1
  git checkout pullrequest/$1
}
```

**Commit and push**
```
gf() {
  git add -A; #add all change into branch
  git commit -m $1;
  branch_name=$(git symbolic-ref --short -q HEAD); #get branch name
  if gd | grep "binding.pry"
  then
    echo "Binding pry detected"
    return 0
  fi
  git push origin $branch_name
}
```

**Commit --amend and force push**
```
gcff() {
  git add -A;
  git commit --amend;
  branch_name=$(git symbolic-ref --short -q HEAD);
  if gd | grep "binding.pry"
  then
    echo "Binding pry detected";
    return 0;
  fi
  git push origin $branch_name -f;
}
```

**Commit --amend --no-edit and force push**
```
gff() {
  git add -A;
  git commit --amend --no-edit;
  branch_name=$(git symbolic-ref --short -q HEAD);
  if gd | grep "binding.pry"
  then
    echo "Binding pry detected";
    return 0;
  fi
  git push origin $branch_name -f;
}
```
