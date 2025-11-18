- [Hashcat](./Hashcat.md)
- [John](./John.md)
- [Crunch](./Crunch.md)
- [Authentication Bruteforcing](./Authentication%20Bruteforcing.md)

## Default Password
If we know the target device, we can search for default passwords and try them. Lists of websites providing default passwords for various products.

https://cirt.net/passwords
https://default-password.info/
https://datarecovery.com/rd/default-passwords/
https://wiki.skullsecurity.org/index.php?title=Passwords

## cewl

```sh
cewl -d 5 -m <length> -w output.txt https://target-website.com
```

**Username Generator**

It is essential to gather employee names during the enumeration stage.
To create a list with most possible combinations based on first name and last name.

```sh
echo "John Smith" > users.lst
python3 username_generator.py -w users.lst
```

```sh
git clone https://github.com/urbanadventurer/username-anarchy.git
cd username-anarchy
./username-anarchy Bill Gates > bill.txt
```

## Password Profiling 
If we know certain details about a specific target, such as their date of birth, pet name, company name, etc., this could be a useful tool for generating passwords based on this known information.

```sh
cupp -i
```

