# Login Server ๐ฐ
- ํ์๊ฐ์๊ณผ ๋ก๊ทธ์ธ ๊ธฐ๋ฅ์ ๊ตฌํํ๊ธฐ ์ํ ์๋ฒ
- ๊ฒ์๋ฌผ์ CRUD๋ฅผ ๊ตฌํํ๊ธฐ ์ํ ์๋ฒ
- MongoDB์ ์ฐ๊ฒฐํ์ฌ ๋ฐ์ดํฐ๋ฒ ์ด์ค์ ์ ์ฅ


๊ฐ๋ฐ ๊ธฐ๊ฐ ๋ฐ ์ฌ์ฉ ๊ธฐ์ 
---
- ๊ฐ๋ฐ ๊ธฐ๊ฐ : 2022.04.20 ~ 2022.05.04

- ์ฌ์ฉ ๊ธฐ์  :  MongoDB, Nodejs, Express


์๋ก ๋ฐฐ์ด ๊ฒ
--- 
- Nodejs Express๋ฅผ ์ด์ฉํด์ ์๋ฒ ๊ตฌ์ฑ
- ํ์๊ฐ์๊ณผ ๋ก๊ทธ์ธ์ ์ํ ๋ฐ์ดํฐ ํต์ 
- MongDB์ ์ฐ๋ํ์ฌ ๋ฐ์ดํฐ ํต์  ๋ฐ ์ ์ฅ
- POST๋ฅผ CRUDํ๊ธฐ ์ํ api ๊ตฌํ
- ๋น๋ฐ๋ฒํธ๋ฅผ Hashํ๊ธฐ
- jwt๋ฅผ ์ด์ฉํ ํ ํฐ ์ธ์ฆ ๋ฐฉ์
- ์ ํจ์ฑ ๊ฒ์ฌ

๊ฒฝํํ๋ ๋ฌธ์ ์ 
---
- ํ์๊ฐ์์ ๊ตฌํํ  ๋ ๋น๋ฐ๋ฒํธ๋ฅผ ์ด๋ป๊ฒ ๋ณด์ํด์ผํ๋์ง ๋ชฐ๋์ง๋ง hash์ฒ๋ฆฌ๋ฅผ ํด์ ๋น๋ฐ๋ฒํธ๋ฅผ ๋ธ์ถ์ํค์ง ์์ ์ ์๋ค๋ ๊ฒ์ ๊นจ๋ฌ์
```
 // Hash password
  const salt = await bcrypt.genSalt(10);
  const hashedPassword = await bcrypt.hash(req.body.password, salt);

  // ์๋ก์ด ์ ์  ๋ง๋ค๊ธฐ
  const user = new User({
    name: req.body.name,
    email: req.body.email,
    password: hashedPassword,
  });
```

- ๋ก๊ทธ์ธํ  ๋ id๊ฐ์ token์ ํ ๋นํ๊ธฐ ์ํด์ ๊ตฌ๊ธ๋ง์ ํตํด ํด๊ฒฐ
```
// ํ ํฐ ์์ฑ ๋ฐ ํ ๋น
    const token = jwt.sign({ _id: user._id }, process.env.TOKEN);
    res.header("auth-token", token).send(token);

    res.status(200).status({ data: token, message: "๋ก๊ทธ์ธ ์ฑ๊ณต" });
  } catch (error) {
    res.status(500).send({ message: "์๋ฒ ์๋ฌ" });
  }
```




