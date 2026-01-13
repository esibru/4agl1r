# Laboratoire PAM

Les lectures suivantes pourront être utiles :

- Morgan, A.G. & Kukuk T. (2005). *The Linux-PAM Guides*  
  http://www.kernel.org/pub/linux/libs/pam/
    - *System Administrators' Guide*  
  http://www.kernel.org/pub/linux/libs/pam/Linux-PAM-html/pam.html
    - *Application Developers' Manual*  
  http://www.kernel.org/pub/linux/libs/pam/Linux-PAM-html/pam_appl.html
- Page de manuel : `man pam`

:::danger Un peu de prudence…
PAM gère toutes les authentifications du système. Soyez prudent !
- Copier le répertoire `pam.d` vers `pam.d.original`
- Réfléchir avant d’agir
:::

## En cas de problèmes

Extrait de Peter WOOD sur [kernel.org](kernel.org) :

> What the hell do I do now?<br/>  
> OK, don't panic. The first thing you have to realize is that this happens to 50% of users who ever do anything with PAM. It happened here, not once, not twice, but three times, all different, and in the end, the solution was the same every time. <br/>
> First, I hope you installed LILO with a delay. If you can, reboot, hit shift or tab or something and type:
>  
> `LILO boot: linux single`
(Replace 'linux' with 'name-of-your-normal-linux-image'). This will let you in without logging in.  Ever wondered how easy it is to break into a linux machine from the console? Now you know.<br/>
> If you can't do that, then get yourself a bootkernel floppy and a root disk a-la slackware's rescue.gz.  (Red Hat's installation disks can be used in this mode too.)<br/>
> In either case, the point is to get back your root prompt.<br/>
> Second, I'm going to assume that you haven't completely nuked your pam installation - just your configuration files. Here's how you make your configs nice again:
>```bash
>cd /etc
>mv pam.conf pam.conf.orig
>mv pam.d pam.d.orig
>mkdir pam.d
>cd pam.d
>```

> and then use vi to create a file called "other" in this directory.  It should contain the following four lines: 
>```bash
>auth     required       pam_unix.so
>account  required       pam_unix.so
>password required       pam_unix.so
>session  required       pam_unix.so
>```

> Now you have the simplest possible PAM configuration that will work the way you're used to.  Everything should magically start to work again.  Try it out by hitting ALT-F2 and logging in on another virtual console.  If it doesn't work, you have bigger problems, or you've mistyped something.  One of the wonders of this system (seriously, perhaps) is that if you mistype anything in the conf files, you usually get no error reporting of any kind on the console - just some entries in the log file.  So look there! (Try 'tail /var/log/messages'.)
From here you can go back and get a real configuration going, hopefully after you've tested it first on a machine you don't care about screwing up.  :/> 

## Manipulations

### Manipulation administrateur

#### Commande `su`

Les premiers exercices s'intéressent à la commande `su` dont la configuration se fait dans `/etc/pam.d/su`. 

:::warning Attention
Ne pas confondre `/usr/bin/su` et `/etc/pam.d/su`: le premier est le binaire `su` tandis que le second est bien son fichier de configuration PAM.
:::

:::info Exercice 1
Modifier `/etc/pam.d/su` pour que `root` entre son mot de passe
:::

:::info Exercice 2
Modifier `/etc/pam.d/su` pour que **aucun utilisateur** n’ait besoin de mot de passe
:::

:::info Exercice 3
Tester ce qui suit en utilisant le _module qui va bien_:

- les restriction « temporelle » : pas de `su` entre 10h15 et 10h30;
- les restriction de « lieu » : pas de `su` d'un terminal, uniquement depuis une console;
- l'un ou l'autre paramètre au choix
:::

… et ensuite tout remettre en ordre


#### Commande `ssh`

Apprenons comment configurer PAM afin qu'il limite l'accès à certains utilisateurs. Nous utiliserons `ssh` pour ce faire. Vérifiez d'abord que vous pouvez vous connecter en ssh à localhost.

Nous allons utiliser le module `pam_listfile.so` (dont vous pouvez lire la doc dans le manuel de l'administrateur PAM). Il faudra donc utiliser cette directive… avec les paramètres qui vont bien.

```config
auth required pam_listfile.so
```

Les paramètres ont une signification. Par exemple, si je ne veux autoriser que les utilisateurs se trouvant listés dans le fichier — que je devrais créer bien sûr — `/etc/pam.d/list-authusers`, je peux écrire;

```ini
auth required pam_listfile.so onerr=succeed item=user \
    sense=allow file=/etc/pam.d/list-auth-users
```

:::tip Exercice 4
Configurez PAM afin que seuls les utilisateurs faisant partie du groupe `ssh` puissent se connecter en ssh à votre machine.
:::

:::info Exercice 5 
Trouver un module intéressant dans la documentation de PAM et le mettre en œuvre.
:::

## Manipulation développeur

Tester et comprendre le programme `check_user.c` du *Application Developers' Manual*.

#### Code source :

```c
#include <security/pam_appl.h>
#include <security/pam_misc.h>
#include <stdio.h>

static struct pam_conv conv = { misc_conv, NULL };

int main(int argc, char *argv[]) {
    pam_handle_t *pamh = NULL;
    int retval;
    const char *user = "nobody";

    if (argc == 2) {
        user = argv[1];
    }
    if (argc > 2) {
        fprintf(stderr, "Usage: check_user [username]\n");
        exit(1);
    }

    retval = pam_start("check_user", user, &conv, &pamh);

    if (retval == PAM_SUCCESS)
        retval = pam_authenticate(pamh, 0);
    if (retval == PAM_SUCCESS)
        retval = pam_acct_mgmt(pamh, 0);
        /* permitted access? */

    /* This is where we have been authorized or not. */

    if (retval == PAM_SUCCESS) {
        fprintf(stdout, "Authenticated\n");
    } else {
        fprintf(stdout, "Not Authenticated\n");
    }

    if (pam_end(pamh, retval) != PAM_SUCCESS) {
        /* close Linux-PAM */
        pamh = NULL;
        fprintf(stderr, "check_user: failed to release authenticator\n");
        exit(1);
    }

    return (retval == PAM_SUCCESS ? 0 : 1);
}
```

Pour rappel, vous devez lier les librairies PAM lors de la compilation… ce qui vous donne une commande du style

```bash
gcc check_user.c -o check_user -lpam -lpam_misc -ldl
```

:::info Exercice 6
Lorsque ce programme compile, ajoutez son fichier de configuration PAM dans le répertoire _qui va bien_ (_aka `/etc/pam.d`) et testez-le.
:::

