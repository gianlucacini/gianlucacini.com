+++
author = "Gianluca Cini"
title = "Localize ASP.NET Identity Error Messages"
date = "2024-02-28"
description = ""

tags = [
    ".net 8", "identity", "asp.net core"
]

draft = false

+++

If you are building an application serving users residing in specific country using ASP.NET Core Identity, it might help knowing how to translate this library's error messages to a specific language.

You can do that by creating a class that inherits IdentityErrorDescriber, then by overriding all its methods.

[Go to my Github Gist](https://gist.github.com/gianlucacini/411fa51d1cc67feb3c9f4f6c6ad3d7e5)


Here is my class which translates default english error messages to italian.

```csharp
using Microsoft.AspNetCore.Identity;

public class ItalianIdentityErrorDescriber : IdentityErrorDescriber
{
   public override IdentityError PasswordRequiresUniqueChars(int uniqueChars) => new IdentityError { Code = nameof(PasswordRequiresUniqueChars), Description = $"La password deve essere contenere almeno {uniqueChars} caratteri univoci." };
   public override IdentityError RecoveryCodeRedemptionFailed() => new IdentityError { Code = nameof(RecoveryCodeRedemptionFailed), Description = $"Il codice di recupero non è stato utilizzato correttamente." };
   public override IdentityError UserNotInRole(string role) => new IdentityError() { Code = nameof(UserNotInRole), Description = $"l'utente non fa parte del ruolo {role}." };
   public override IdentityError DefaultError() => new IdentityError { Code = nameof(DefaultError), Description = $"Si è verificato un errore sconosciuto." };
   public override IdentityError ConcurrencyFailure() => new IdentityError { Code = nameof(ConcurrencyFailure), Description = "Fallimento della concorrenza ottimistica, l'oggetto è stato modificato." };
   public override IdentityError PasswordMismatch() => new IdentityError { Code = nameof(PasswordMismatch), Description = "Password non corretta." };
   public override IdentityError InvalidToken() => new IdentityError { Code = nameof(InvalidToken), Description = "Token non valido" };
   public override IdentityError LoginAlreadyAssociated() => new IdentityError { Code = nameof(LoginAlreadyAssociated), Description = "Esiste già un utente con questo login." };
   public override IdentityError InvalidEmail(string? email) => new IdentityError { Code = nameof(InvalidEmail), Description = $"Email '{email}' non è valida." };
   public override IdentityError InvalidRoleName(string? role) => new IdentityError { Code = nameof(InvalidRoleName), Description = $"Il Ruolo '{role}' non è valido." };
   public override IdentityError InvalidUserName(string? userName) => new IdentityError { Code = nameof(InvalidUserName), Description = $"Il nome utente '{userName}' non è valido, utilizzare i caratteri 'a-z 'A-Z'." };
   public override IdentityError DuplicateUserName(string userName) => new IdentityError { Code = nameof(DuplicateUserName), Description = $"Il nome utente '{userName}' è già stato preso." };
   public override IdentityError DuplicateEmail(string email) => new IdentityError { Code = nameof(DuplicateEmail), Description = $"l'email '{email}' è già stata presa." };
   public override IdentityError DuplicateRoleName(string role) => new IdentityError { Code = nameof(DuplicateRoleName), Description = $"il ruolo '{role}' è già stato preso." };
   public override IdentityError UserAlreadyHasPassword() => new IdentityError { Code = nameof(UserAlreadyHasPassword), Description = "L'utente ha già impostato una password." };
   public override IdentityError UserLockoutNotEnabled() => new IdentityError { Code = nameof(UserLockoutNotEnabled), Description = "Il blocco non è abilitato per questo utente." };
   public override IdentityError UserAlreadyInRole(string role) => new IdentityError { Code = nameof(UserAlreadyInRole), Description = $"L'utente è già nel ruolo '{role}'." };
   public override IdentityError PasswordTooShort(int length) => new IdentityError { Code = nameof(PasswordTooShort), Description = $"Le password devono avere almeno {length} caratteri." };
   public override IdentityError PasswordRequiresNonAlphanumeric() => new IdentityError { Code = nameof(PasswordRequiresNonAlphanumeric), Description = "Le password devono contenere almeno un carattere non alfanumerico." };
   public override IdentityError PasswordRequiresDigit() => new IdentityError { Code = nameof(PasswordRequiresDigit), Description = "Le password devono contenere almeno una cifra ('0'-'9')." };
   public override IdentityError PasswordRequiresLower() => new IdentityError { Code = nameof(PasswordRequiresLower), Description = "Le password devono contenere almeno una lettera minuscola ('a'-'z')." };
   public override IdentityError PasswordRequiresUpper() => new IdentityError { Code = nameof(PasswordRequiresUpper), Description = "Le password devono contenere almeno una lettera maiuscola ('A'-'Z')." };
}

```

Then, in your Program.cs, add your class to the IdentityBuilder configuration

```csharp

builder.Services
   .AddIdentity<ApplicationUser, IdentityRole>().AddErrorDescriber<ItalianIdentityErrorDescriber>()
   .AddEntityFrameworkStores<ApplicationDbContext>()
   .AddDefaultTokenProviders();

```