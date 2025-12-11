import random

class SacADos:
    def __init__(self, valeurs, poids, capacite):
        self.valeurs = valeurs
        self.poids = poids
        self.capacite = capacite
        self.n = len(valeurs)

    def eval(self, sol):
        valeur = sum(sol[i] * self.valeurs[i] for i in range(self.n))
        poids_total = sum(sol[i] * self.poids[i] for i in range(self.n))
        return valeur, poids_total, poids_total <= self.capacite

def solution_aleatoire_valide(probleme):
    sol = [0] * probleme.n
    indices = list(range(probleme.n))
    random.shuffle(indices)
    poids = 0
    for i in indices:
        if poids + probleme.poids[i] <= probleme.capacite:
            sol[i] = 1
            poids += probleme.poids[i]
    return sol

def hill_climbing(probleme, max_iter=5000):
    sol = solution_aleatoire_valide(probleme)
    best_val, best_poids, _ = probleme.eval(sol)
    for _ in range(max_iter):
        i = random.randint(0, probleme.n - 1)
        voisin = sol.copy()
        voisin[i] = 1 - voisin[i]
        val, poids, ok = probleme.eval(voisin)
        if ok and val > best_val:
            sol = voisin
            best_val = val
            best_poids = poids
    return sol, best_val, best_poids

def afficher(solution, valeurs, poids, capacite):
    objets = [i for i in range(len(solution)) if solution[i] == 1]
    valeur_totale = sum(valeurs[i] for i in objets)
    poids_total = sum(poids[i] for i in objets)
    print("\n=== SOLUTION HILL CLIMBING ===")
    for i in objets:
        print(f"Objet {i+1} → valeur={valeurs[i]}, poids={poids[i]}")
    print("------------------------------")
    print(f"Valeur totale : {valeur_totale}")
    print(f"Poids total   : {poids_total} / {capacite}")
    print(f"Utilisation   : {poids_total/capacite*100:.1f}%")

if __name__ == "__main__":
    valeurs = [10, 5, 15, 7, 6, 18, 3, 12, 8, 14]
    poids   = [ 2, 3, 5, 7, 1, 4, 1, 6, 3, 8]
    capacite = 20

    probleme = SacADos(valeurs, poids, capacite)
    solution, val, p = hill_climbing(probleme, max_iter=3000)
    afficher(solution, valeurs, poids, capacite)
