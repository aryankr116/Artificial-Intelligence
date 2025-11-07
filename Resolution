from itertools import combinations

def resolve(ci, cj):
    """Return resolvents of two clauses."""
    resolvents = set()
    for di in ci:
        for dj in cj:
            if di == '~' + dj or dj == '~' + di:
                new_clause = (ci - {di}) | (cj - {dj})
                resolvents.add(frozenset(new_clause))
    return resolvents

def pl_resolution(kb, query):
    """Propositional logic resolution algorithm."""
    clauses = kb.copy()
    clauses.append({f'~{query}'})  # add negation of query
    new = set()

    while True:
        n = len(clauses)
        pairs = list(combinations(range(n), 2))

        for (i, j) in pairs:
            resolvents = resolve(clauses[i], clauses[j])
            if frozenset() in resolvents:
                return True  # Empty clause found — query proven
            new |= resolvents

        if new.issubset(set(map(frozenset, clauses))):
            return False  # No new information — not provable

        for c in new:
            if c not in clauses:
                clauses.append(set(c))

# --- Complex Knowledge Base ---
kb = [
    {'~R', 'W'},  # R → W
    {'~S', 'W'},  # S → W
    {'~W', 'G'},  # W → G
    {'S'}         # Sprinkler is on
]

query = 'G'  # Is the grass slippery?

if pl_resolution(kb, query):
    print(f"The query '{query}' is entailed by the knowledge base.")
else:
    print(f"The query '{query}' is NOT entailed by the knowledge base.")
