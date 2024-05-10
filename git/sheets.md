# config

```sh
git config --global user.name "Nick Georgi"
```

```sh
git config --global user.email "Nick.Georgi@telekom.de"
```

show config

```sh
git config user.name
```

```sh
git config user.email
```

---
clone or connect

```sh
git clone https://git.t-systems-mms.com/scm/~ncgo/test.git
```

add new files

```sh
git add --all
```

comment

```sh
git commit -m "Initial Commit"
```

push

```sh
git push -u origin
```

---

if you already have code

```sh
cd existing-project
git init
git add --all
git commit -m "Initial Commit"
git remote add origin https://git.t-systems-mms.com/scm/~ncgo/test.git
git push -u origin HEAD:main
```

---

change branch

```sh
git checkout desiredbranch
```
