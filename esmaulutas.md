class Library:
    def __init__(self):
        self.file_name = "books.txt"
        self.file = open(self.file_name, "a+")
    def __del__(self):
        self.file.close()
    def list_books(self):
        self.file.seek(0)
        books = self.file.readlines()
        for book in books:
            book_info = book.strip().split(',')
            print("Kitap Adı: {}, Yazarı: {}".format(book_info[0], book_info[1]))
    def add_book(self):
        title = input("Kitap adını girin: ").lower()  # Girişin tamamen küçük harfe dönüştürülmesi
        author = input("Kitabın yazarını girin: ")
        release_year = input("İlk yayın yılını girin: ")
        num_pages = input("Sayfa sayısını girin: ")
        book_info = "{},{},{},{}\n".format(title, author, release_year, num_pages)
        self.file.write(book_info)
        print("Kitap başarıyla eklendi.")
    def remove_book(self):
        title = input("Silmek istediğiniz kitabın başlığını girin: ").lower()  # Girişin tamamen küçük harfe dönüştürülmesi
        self.file.seek(0)
        books = self.file.readlines()
        updated_books = []
        removed = False
        for book in books:
            book_info = book.strip().split(',')
            if book_info[0].lower() != title:  # Karşılaştırma için girişin tamamen küçük harfe dönüştürülmesi
                updated_books.append(book)
            else:
                removed = True
        if removed:
            self.file.seek(0)
            self.file.truncate()
            self.file.writelines(updated_books)
            print("Kitap başarıyla silindi.")
        else:
            print("Kitap bulunamadı.")
lib = Library()
while True:
    print("\n*** MENÜ ***")
    print("1) Kitapları Listele")
    print("2) Kitap Ekle")
    print("3) Kitap Sil")
    print("4) q (Çıkış)")
    choice = input("Lütfen seçiminizi yapın (1/2/3/4): ")
    if choice == '1':
        lib.list_books()
    elif choice == '2':
        lib.add_book()
    elif choice == '3':
        lib.remove_book()
    elif choice == '4' or choice.lower() == 'q':
        print("Programdan çıkılıyor...")
        break
    else:
        print("Geçersiz seçim. Lütfen 1, 2, 3 veya 4'ü seçin.")
