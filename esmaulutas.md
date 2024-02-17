class Library:
    def __init__(self):
        self.books_file = open("books.txt", "a+")
    def __del__(self):
        self.books_file.close()
    def list_books(self):
        with open("books.txt", "r") as f:
            books = f.readlines()
        for book in books:
            print(f"Kitap Adı: {book.split(',')[0]}")
            print(f"Yazar: {book.split(',')[1]}")
    def add_book(self):
        book_name = input("Kitap Adı: ").lower()
        author = input("Yazar: ")
        release_year = int(input("Yayın Yılı: "))
        page_count = int(input("Sayfa Sayısı: "))
        book_info = f"{book_name},{author},{release_year},{page_count}\n"
        self.books_file.write(book_info)
    def remove_book(self):
        book_title = input("Silinecek Kitap Adı: ").lower()
        with open("books.txt", "r") as f:
            books = f.readlines()
        book_index = -1
        for i, book in enumerate(books):
            if book_title in book.lower():
                book_index = i
                break
        if book_index != -1:
            books.pop(book_index)
            with open("books.txt", "w") as f:
                f.writelines(books)
        else:
            print(f"{book_title} adlı kitap bulunamadı.")

lib = Library()

while True:
    print("""
*** MENÜ ***
1) Kitapları Listele
2) Kitap Ekle
3) Kitap Sil
q) Çıkış
""")

    menu_item = input("Seçiminizi giriniz: ")

    if menu_item == "1":
        lib.list_books()
    elif menu_item == "2":
        lib.add_book()
    elif menu_item == "3":
        lib.remove_book()
    elif menu_item == "q":
        break
    else:
        print("Geçersiz seçim.")

print("Programdan çıkılıyor...")
