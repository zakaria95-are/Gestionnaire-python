# ============================
#   MINI GESTIONNAIRE D’UTILISATEURS
# ============================

utilisateurs = []


# --- Hachage du mot de passe (inversion) ---
def hash_mdp(mdp):
    return mdp[::-1]


# --- Ajouter un utilisateur ---
def ajouter_utilisateur():
    nom = input("Nom : ")
    email = input("Email : ")
    mdp = input("Mot de passe : ")

    utilisateur = {
        "nom": nom,
        "email": email,
        "mdp": hash_mdp(mdp)
    }

    utilisateurs.append(utilisateur)
    print("Utilisateur ajouté !")


# --- Afficher les utilisateurs ---
def afficher_utilisateurs():
    if not utilisateurs:
        print("Aucun utilisateur enregistré.")
        return

    for i, user in enumerate(utilisateurs):
        print(f"{i} - {user['nom']} | {user['email']} | {user['mdp']}")


# --- Modifier un utilisateur ---
def modifier_utilisateur():
    afficher_utilisateurs()
    try:
        index = int(input("Index de l’utilisateur à modifier : "))
        if index < 0 or index >= len(utilisateurs):
            print("Index invalide.")
            return
    except:
        print("Entrée invalide.")
        return

    nom = input("Nouveau nom : ")
    email = input("Nouvel email : ")
    mdp = input("Nouveau mot de passe : ")

    utilisateurs[index]["nom"] = nom
    utilisateurs[index]["email"] = email
    utilisateurs[index]["mdp"] = hash_mdp(mdp)

    print("Utilisateur modifié !")


# --- Supprimer un utilisateur ---
def supprimer_utilisateur():
    afficher_utilisateurs()
    try:
        index = int(input("Index de l’utilisateur à supprimer : "))
        if index < 0 or index >= len(utilisateurs):
            print("Index invalide.")
            return
    except:
        print("Entrée invalide.")
        return

    utilisateurs.pop(index)
    print("Utilisateur supprimé !")


# --- Connexion ---
def connexion():
    email = input("Email : ")
    mdp = input("Mot de passe : ")

    mdp_hache = hash_mdp(mdp)

    for user in utilisateurs:
        if user["email"] == email and user["mdp"] == mdp_hache:
            print("Connexion réussie !")
            return

    print("Échec : identifiants incorrects.")


# --- MENU PRINCIPAL ---
def menu():
    while True:
        print("\n===== Gestionnaire Utilisateurs =====")
        print("1 - Ajouter un utilisateur")
        print("2 - Liste des utilisateurs")
        print("3 - Modifier un utilisateur")
        print("4 - Supprimer un utilisateur")
        print("5 - Connexion")
        print("6 - Quitter")

        choix = input("Votre choix : ")

        if choix == "1":
            ajouter_utilisateur()
        elif choix == "2":
            afficher_utilisateurs()
        elif choix == "3":
            modifier_utilisateur()
        elif choix == "4":
            supprimer_utilisateur()
        elif choix == "5":
            connexion()
        elif choix == "6":
            print("Au revoir !")
            break
        else:
            print("Choix invalide.")


menu()

