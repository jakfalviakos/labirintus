import random
 
MERETX = 35
MERETY = 15
 
FAL = '#'
JARAT = ' '
 
 
# Kétdimenziós lista az előadásról
def ketdimenzios(szeles, magas, kezdeti=None):
    palya = []
    for _ in range(magas):
        palya.append([kezdeti]*szeles)
    return palya
 
 
# kirajzolás
def kirajzol(palya):
    for y in range(MERETY):
        for x in range(MERETX):
            print(palya[y][x], end='')
        print()
 
 
# maga a generáló függvény
def labirintus(palya, x, y):
    FEL = 1
    BALRA = 2
    LE = 3
    JOBBRA = 4
 
    # erre a pontra hívtak minket, ide lerakunk egy darabka járatot
    palya[y][x] = JARAT
 
    # irányok keverése
    iranyok = [FEL, BALRA, LE, JOBBRA]
    random.shuffle(iranyok)
 
    # a kevert irányok szerint mindenfelé próbálunk menni, ha lehet.
    for irany in iranyok:
        if irany == FEL:
            if y >= 2 and palya[y - 2][x] != JARAT:
                palya[y - 1][x] = JARAT        # elindítjuk arrafelé a járatot
                labirintus(palya, x, y - 2)    # es rekurzíve megyünk tovább
 
        elif irany == BALRA:
            if x >= 2 and palya[y][x - 2] != JARAT:
                palya[y][x - 1] = JARAT
                labirintus(palya, x - 2, y)
 
        elif irany == LE:
            if y < MERETY - 2 and palya[y + 2][x] != JARAT:
                palya[y + 1][x] = JARAT
                labirintus(palya, x, y + 2)
 
        elif irany == JOBBRA:
            if x < MERETX - 2 and palya[y][x + 2] != JARAT:
                palya[y][x + 1] = JARAT
                labirintus(palya, x + 2, y)
 
 
def main():
    # üres pálya létrehozása
    palya = ketdimenzios(MERETX, MERETY, FAL)
 
    # labirintus generálása
    labirintus(palya, 1, 1)
 
    # be- és kijárat
    palya[1][0] = JARAT
    palya[MERETY - 2][MERETX - 1] = JARAT
 
    # és mehet kirajzolásra
    kirajzol(palya)
 
 
main()
