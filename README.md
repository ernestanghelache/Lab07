## 1. De ce Logout este implementat ca <form method="post"> și nu ca un link <a href="/Auth/Logout">?

Logout-ul trebuie sa fie POST si nu GET din motive de securitate, pentru a preveni atacurile CSRF sau delogarile involuntare.


## 2. De ce login-ul face doi pași în loc de unul?

`csharp
var user = await _userManager.FindByEmailAsync(model.Email);  // pasul 1
var result = await _signInManager.PasswordSignInAsync(user.UserName!, ...);  // pasul 2
`
Username-ul este cheia primara pentru autentificare în Identity, iar email este doar un camp secundar. De aceea, trebuie sa cautam utilizatorul dupa email pentru a obtine username, care este apoi folosit pentru autentificare.

## 3. De ce nu este suficient sa ascunzi butoanele Edit/Delete în View?

Acesta nu ofera securitate, deoarece ar putea fi accesat prin link fara probleme.

## 4. Ce este middleware pipeline-ul în ASP.NET Core?

Middleware pipeline-ul este o serie de componente care proceseaza HTTP requests în ordine, ca o linie de asamblare.
UseAuthentication() trebuie pus inainte de UseAuthorization(), daca inversezi ordinea, UseAuthorization va verifica permisiuni pe un User NULL

## 5. Ce am fi trebuit sa implementam manual daca nu foloseam ASP.NET Core Identity?
- Autentificare
- Inregistrare utilizatori
- Siguranta parolelor

## 6. Care sunt dezavantajele folosirii ASP.NET Core Identity?

- Aplicatiile de mobil nu pot folosi cookies
- Greu de implementat scenarii avansate cum ar fi social login
- Nu functioneaza cu NoSQL
