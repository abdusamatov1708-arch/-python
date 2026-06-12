# -python
kontaktlar = {
    "Sunnat": {"tel": "+500052636", "manzil": "Chirchiq", "email": "abdusamatov1707@gmail.com"},
    "Jasur": {"tel": "+880012717", "manzil": "Chirchiq", "email": "jasur13032011@gmail.com"},
    "Kamron": {"tel": "+975448431", "manzil": "Toshkent", "email": "onlykamron@gmail.com"}
}


def kontakt_qoshish(ism, tel, manzil, email):
    if not ism or not ism.strip():
        print("Xato: Ism bo'sh bo'lishi mumkin emas!")
        return

    toza_tel = tel.replace(" ", "").replace("-", "")
    if not toza_tel.startswith("+") or not toza_tel[1:].isdigit():
        print(f"Xato: '{tel}' noto'g'ri telefon raqami!")
        return

    kontaktlar[ism] = {"tel": tel, "manzil": manzil, "email": email}
    print(f"Kontakt '{ism}' muvaffaqiyatli qo'shildi.")


def kontakt_qidirish(kalit_soz):
    topildi = []
    for ism, malumot in kontaktlar.items():
        if kalit_soz.lower() in ism.lower() or kalit_soz in malumot["tel"]:
            topildi.append((ism, malumot))

    if topildi:
        for ism, malumot in topildi:
            print(f"Topildi: {ism} | Tel: {malumot['tel']} | Manzil: {malumot['manzil']} | Email: {malumot['email']}")
    else:
        print("Hech qanday kontakt topilmadi.")


def kontakt_ochirish(ism):
    if ism in kontaktlar:
        del kontaktlar[ism]
        print(f"Kontakt '{ism}' o'chirildi.")
    else:
        print(f"Xato: '{ism}' ismli kontakt topilmadi.")


def hammasini_korsatish():
    print("\n--- Barcha Kontaktlar ---")
    tartiblangan_kalitlar = sorted(kontaktlar.keys())
    for ism in tartiblangan_kalitlar:
        m = kontaktlar[ism]
        print(f"{ism} -> Tel: {m['tel']}, Manzil: {m['manzil']}, Email: {m['email']}")


def statistika_chiqarish():
    jami = len(kontaktlar)
    if jami > 0:
        eng_uzun_ism = max(kontaktlar.keys(), key=len)
    else:
        eng_uzun_ism = "Yo'q"
    print(f"\n--- Statistika ---\nJami kontaktlar: {jami}\nEng uzun ism: {eng_uzun_ism}")


def unikal_shaharlar():
    shaharlar = {malumot["manzil"] for malumot in kontaktlar.values()}
    print(f"\nUnikal shaharlar ro'yxati: {shaharlar}")


def shaharga_kora_filtrla(shahar_nomi):
    toshkentliklar = {ism: malumot for ism, malumot in kontaktlar.items() if
                      malumot["manzil"].lower() == shahar_nomi.lower()}
    print(f"\n--- {shahar_nomi}dagi kontaktlar ---")
    for ism, m in toshkentliklar.items():
        print(f"{ism} : {m['tel']}")




kontakt_qoshish("", "901234567", "Buxoro", "test@mail.ru")
kontakt_qoshish("Jasur", "abcd", "Farg'ona", "h@mail.ru")

kontakt_qoshish("Dilshod", "+991112233", "Namangan", "dilshod@gmail.com")

hammasini_korsatish()
statistika_chiqarish()
unikal_shaharlar()

print("\n--- Qidirish natijasi ---")
kontakt_qidirish("91")
kontakt_qidirish("ali") 

shaharga_kora_filtrla("Toshkent")

kontakt_ochirish("Ali")
hammasini_korsatish()
