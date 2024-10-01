# config

```sh
git config --global user.name "your name"
```

```sh
git config --global user.email "your.mail"
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
git clone https://...
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
git remote add origin https://
git push -u origin HEAD:main
```

---

change branch

```sh
git checkout desiredbranch
```
