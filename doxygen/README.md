# Ćwiczenie 4
Repozytorium z plikami wykorzystanymi w ćwiczeniu: [link](https://github.com/alkatraz445/SiNWO_4)

## `main.py`
```py
class Queue:
    """Klasa reprezentująca kolejkę.

    Kolejka to struktura danych,
    która działa na zasadzie "first in, first out" (FIFO).
    Elementy są dodawane na końcu kolejki 
    i usuwane z początku kolejki.

    Attributes:
        items (list): Lista przechowująca elementy kolejki.

    Methods:
        enqueue(item): Dodaje element na koniec kolejki.
        dequeue(): Usuwa i zwraca element z początku kolejki.
        is_empty(): Sprawdza, czy kolejka jest pusta.
        size(): Zwraca liczbę elementów w kolejce.
    """

    def __init__(self):
        """Inicjalizuje pustą kolejkę."""
        self.items = []

    def enqueue(self, item):
        """Dodaje element na koniec kolejki.

        Args:
            item: Element do dodania do kolejki.
        """
        self.items.append(item)

    def dequeue(self):
        """Usuwa i zwraca element z początku kolejki.

        Returns:
            Element z początku kolejki.
        """
        if not self.is_empty():
            return self.items.pop(0)
        else:
            raise IndexError("Dequeue from an empty queue")

    def is_empty(self):
        """Sprawdza, czy kolejka jest pusta.

        Returns:
            True, jeśli kolejka jest pusta;
            False w przeciwnym razie.
        """
        return len(self.items) == 0

    def size(self):
        """Zwraca liczbę elementów w kolejce.

        Returns:
            Liczba elementów w kolejce.
        """
        return len(self.items)

# Przykłady użycia
if __name__ == "__main__":
    my_queue = Queue()

    my_queue.enqueue(1)
    my_queue.enqueue(2)
    my_queue.enqueue(3)

    print("Size of the queue:", my_queue.size())
    print("Dequeue:", my_queue.dequeue())
    print("Is the queue empty?", my_queue.is_empty())
```
