# proje1
import tkinter as tk
import numpy as np
def change_theme_dark():
    root.configure(bg='black')
    label.configure(bg='black', fg='white')
    button.configure(bg='gray', fg='black')

root = tk.Tk()
root.configure(bg='light blue')

label = tk.Label(root, text="Ana ekranı kapatmaya yarar")
label.pack()
def kapat():
    root.destroy()

kapat_button = tk.Button(root, text="Kapat", bg='blue', command=kapat)
kapat_button.pack()
root = tk.Tk()
button = tk.Button(root, text="Karanlık Tema", bg='blue', command=change_theme_dark)
button.pack()
def k_kucuk_ui():
    k = int(entry_k.get())
    sayilar_x = entry_sayilar.get()
    sayilar = [int(sayi) for sayi in sayilar_x.split(",")]

    sonuc = k_kucuk(k, sayilar)
    if sonuc is not None:
        sonuc_label_kucuk.config(text=f"{k}. en küçük eleman: {sonuc}")
    else:
        sonuc_label_kucuk.config(text="Listede o kadar eleman yok")
def k_kucuk(k, sayilar):
    if len(sayilar) < k:
        return None

    sayilar.sort()
    return sayilar[k - 1]

def en_yakin_cift_ui():
    hedef = int(entry_hedef.get())
    sayilar_x = entry_cift_sayilar.get()
    sayilar = [int(sayi) for sayi in sayilar_x.split(",")]

    sonuc = en_yakin_cift(hedef, sayilar)
    sonuc_label_cift.config(text=f"En yakın çift: {sonuc[0]} ve {sonuc[1]}")
def en_yakin_cift(hedef, sayilar):
    sayilar.sort()
    min_fark = float('inf')
    en_yakin_cift = None

    for i in range(len(sayilar) - 1):
        fark = abs(sayilar[i] + sayilar[i + 1] - hedef)
        if fark < min_fark:
            min_fark = fark
            en_yakin_cift = (sayilar[i], sayilar[i + 1])

    return en_yakin_cift

def tekrar_eden_elemanlar_ui():
    liste_x = entry_liste.get()
    liste = [int(eleman) for eleman in liste_x.split(",")]

    sonuc = tekrar_eden_elemanlar(liste)
    sonuc_label_tekrar_eden.config(text=f"Tekrar eden elemanlar: {sonuc}")
def tekrar_eden_elemanlar(liste):
    frekanslar = {}
    tekrar_edenler = []

    for eleman in liste:
        if eleman in frekanslar:
            frekanslar[eleman] += 1
        else:
            frekanslar[eleman] = 1

    for eleman, frekans in frekanslar.items():
        if frekans > 1:
            tekrar_edenler.append(eleman)

    return tekrar_edenler
def matris_multiply_ui():
    matris1_x = entry_matris1.get()
    matris2_x = entry_matris2.get()

    matris1 = [list(map(int, row.split(","))) for row in matris1_x.split(";")]
    matris2 = [list(map(int, row.split(","))) for row in matris2_x.split(";")]

    sonuc = matris_multiply(matris1, matris2)
    if sonuc is not None:
        sonuc_label_matris.config(text="\n".join([" ".join(map(str, row)) for row in sonuc]))
    else:
        sonuc_label_matris.config(text="Matris boyutları çarpılabilir değil.")
def matris_multiply(matris1, matris2):
    m1_rows = len(matris1)
    m1_cols = len(matris1[0])
    m2_rows = len(matris2)
    m2_cols = len(matris2[0])

    if m1_cols != m2_rows:
        return None

    sonuc = [[0 for _ in range(m2_cols)] for _ in range(m1_rows)]

    for i in range(m1_rows):
        for j in range(m2_cols):
            for k in range(m2_rows):
                sonuc[i][j] += matris1[i][k] * matris2[k][j]

    return sonuc
def kelime_frekans_ui():
    text = entry_metin.get()

    sonuc = kelime_frekansi(text)
    sonuc_label_kelimeler.config(text="\n".join([f"{word}={freq}" for word, freq in sonuc.items()]))
def kelime_frekansi(metin):
    kelimeler = metin.split()

    frekanslar = {}
    for kelime in kelimeler:
        kelime = kelime.lower()
        if kelime in frekanslar:
            frekanslar[kelime] += 1
        else:
            frekanslar[kelime] = 1

    return frekanslar

def en_kucuk_deger_ui():
    liste_x = entry_liste_kucuk.get()
    liste = [int(eleman) for eleman in liste_x.split(",")]

    sonuc = en_kucuk_deger(liste)
    sonuc_label_kucuk_deger.config(text=f"En küçük değer: {sonuc}")
def en_kucuk_deger(liste):
    if len(liste) == 0:
        return None

    min_deger = min(liste)
    return min_deger

def karekok_ui():
    N = float(entry_N.get())
    x0 = float(entry_x0.get())

    sonuc = karekok(N, x0)
    sonuc_label_karekok.config(text=sonuc)
def en_kucuk_deger(liste):
    if len(liste) == 0:
        return None

    min_deger = min(liste)
    return min_deger

def eb_ortak_bolen_ui():
    a = int(entry_a.get())
    b = int(entry_b.get())

    sonuc = eb_ortak_bolen(a, b)
    sonuc_label_eb.config(text=f"En büyük ortak bölen: {sonuc}")
def eb_ortak_bolen(a, b):
    while b:
        a, b = b, a % b
    return a

def asal_veya_degil_ui():
    n = int(entry_asal.get())

    sonuc = asal_veya_degil(n)
    sonuc_label_asal.config(text=f"Asal sayı mı? {sonuc}")
def asal_veya_degil(n):
    if n <= 1:
        return False
    if n <= 3:
        return True

    if n % 2 == 0 or n % 3 == 0:
        return False

    i = 5
    while i * i <= n:
        if n % i == 0 or n % (i + 2) == 0:
            return False
        i += 6

    return True

def fibonacci_hizlandirici_ui():
    n = int(entry_n_fibonacci.get())

    sonuc = fibonacci_hizlandirici(n, 1, 1, 0)
    sonuc_label_fibonacci.config(text=sonuc)
def fibonacci_hizlandirici(n, a=0, b=1, i=0):
    if n == i:
        return a

    return fibonacci_hizlandirici(n, b, a + b, i + 1)

root.title("İşlev Seçici")
root.configure(bg='light blue')
k_label = tk.Label(root, text="K'nıncı Küçük Sayıyı Bulma")
k_label.pack()

entry_k = tk.Entry(root)
entry_k.pack()

entry_sayilar = tk.Entry(root)
entry_sayilar.pack()

k_button = tk.Button(root, text="K'nıncı Küçük Sayıyı Bul",bg='blue',  command=k_kucuk_ui)
k_button.pack()

sonuc_label_kucuk = tk.Label(root, text="")
sonuc_label_kucuk.pack()

cift_label = tk.Label(root, text="En Yakın Çifti Bulma")
cift_label.pack()

entry_hedef = tk.Entry(root)
entry_hedef.pack()

entry_cift_sayilar = tk.Entry(root)
entry_cift_sayilar.pack()

cift_button = tk.Button(root, text="En Yakın Çifti Bul", bg='blue', command=en_yakin_cift_ui)
cift_button.pack()

sonuc_label_cift = tk.Label(root, text="")
sonuc_label_cift.pack()

tekrar_eden_label = tk.Label(root, text="Tekrar Eden Elemanları Bulma")
tekrar_eden_label.pack()

entry_liste = tk.Entry(root)
entry_liste.pack()

tekrar_eden_button = tk.Button(root, text="Tekrar Eden Elemanları Bul",bg='blue',  command=tekrar_eden_elemanlar_ui)
tekrar_eden_button.pack()

sonuc_label_tekrar_eden = tk.Label(root, text="")
sonuc_label_tekrar_eden.pack()

matris_label = tk.Label(root, text="Matris Çarpımı")
matris_label.pack()

matris1_label = tk.Label(root, text="Matris 1 (satır sütun):")
matris1_label.pack()

entry_matris1 = tk.Entry(root)
entry_matris1.pack()

matris2_label = tk.Label(root, text="Matris 2 (satır sütun):")
matris2_label.pack()

entry_matris2 = tk.Entry(root)
entry_matris2.pack()

matris_button = tk.Button(root, text="Matris Çarpımı Yap", bg='blue', command=matris_multiply_ui)
matris_button.pack()

sonuc_label_matris = tk.Label(root, text="")
sonuc_label_matris.pack()

kelime_frekans_label = tk.Label(root, text="Kelime Frekansı Bulma")
kelime_frekans_label.pack()

entry_metin = tk.Entry(root)
entry_metin.pack()

kelime_frekans_button = tk.Button(root, text="Kelime Frekansını Hesapla", bg='blue', command=kelime_frekans_ui)
kelime_frekans_button.pack()

sonuc_label_kelimeler = tk.Label(root, text="")
sonuc_label_kelimeler.pack()

kucuk_deger_label = tk.Label(root, text="En Küçük Değer Bulma")
kucuk_deger_label.pack()

entry_liste_kucuk = tk.Entry(root)
entry_liste_kucuk.pack()

kucuk_deger_button = tk.Button(root, text="En Küçük Değeri Bul", bg='blue', command=en_kucuk_deger_ui)
kucuk_deger_button.pack()

sonuc_label_kucuk_deger = tk.Label(root, text="")
sonuc_label_kucuk_deger.pack()

karekok_label = tk.Label(root, text="Karekök Bulma (Babil Yöntemi)")
karekok_label.pack()

entry_N = tk.Entry(root)
entry_N.pack()

entry_x0 = tk.Entry(root)
entry_x0.pack()

karekok_button = tk.Button(root, text="Karekökü Bul",bg='blue',  command=karekok_ui)
karekok_button.pack()

sonuc_label_karekok = tk.Label(root, text="")
sonuc_label_karekok.pack()

eb_ortak_bolen_label = tk.Label(root, text="En Büyük Ortak Bölen Bulma")
eb_ortak_bolen_label.pack()

entry_a = tk.Entry(root)
entry_a.pack()

entry_b = tk.Entry(root)
entry_b.pack()

eb_button = tk.Button(root, text="En Büyük Ortak Böleni Bul",bg='blue',  command=eb_ortak_bolen_ui)
eb_button.pack()

sonuc_label_eb = tk.Label(root, text="")
sonuc_label_eb.pack()

asal_label = tk.Label(root, text="Asal Sayı Kontrolü")
asal_label.pack()

entry_asal = tk.Entry(root)
entry_asal.pack()

asal_button = tk.Button(root, text="Asal Sayı Mı?", bg='blue', command=asal_veya_degil_ui)
asal_button.pack()

sonuc_label_asal = tk.Label(root, text="")
sonuc_label_asal.pack()

fibonacci_label = tk.Label(root, text="Fibonacci Hesaplama (Hızlandırılmış)")
fibonacci_label.pack()

entry_n_fibonacci = tk.Entry(root)
entry_n_fibonacci.pack()

fibonacci_button = tk.Button(root, text="Fibonacci Hesapla", bg='blue',command=fibonacci_hizlandirici_ui)
fibonacci_button.pack()

sonuc_label_fibonacci = tk.Label(root, text="")
sonuc_label_fibonacci.pack()

root.mainloop()
