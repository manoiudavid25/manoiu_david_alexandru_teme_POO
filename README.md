# manoiu_david_alexandru_teme_POO
Să se implementeze în C++ clasa ⁠Librarie⁠ care conține un identificator constant, o denumire, un număr de cărți și un pointer pentru prețurile stocate în heap. Clasa va include constructor implicit, constructor cu parametri, constructor de copiere (pentru Deep Copy), destructor, o variabilă statică pentru contorizarea obiectelor și o metodă de afișare.

#include <iostream>
#include <string>

using namespace std;

class Librarie {
private:
	const int id;
	string denumire;
	int nrCarti;
	float* vectorPreturi;
public:
	static int nrLibrarii;

	Librarie() : id(++nrLibrarii) {
		this->denumire = "Default";
		this->nrCarti = 0;
		this->vectorPreturi = nullptr;
	}

	Librarie(int id, string denumire, int nrCarti, float* vectorPreturi) : id(id) {
		this->denumire = denumire;
		this->nrCarti = nrCarti;
		this->vectorPreturi = new float[nrCarti];
		for (int i = 0; i < this->nrCarti; i++) {
			this->vectorPreturi[i] = vectorPreturi[i];
		}
		nrLibrarii++;
	}

	Librarie(const Librarie& l) : id(l.id) {
		this->denumire = l.denumire;
		this->nrCarti = l.nrCarti;
		this->vectorPreturi = new float[l.nrCarti];
		for (int i = 0; i < this->nrCarti; i++) {
			this->vectorPreturi[i] = l.vectorPreturi[i];
		}
	}

	~Librarie() {
		if (this->vectorPreturi != nullptr) {
			delete[] this->vectorPreturi;
		}
	}

	void afisare() {
		cout << "\nId: " << this->id << ", Denumire: " << this->denumire << ", Nr carti: " << this->nrCarti;
		if (this->nrCarti > 0) {
			cout << ", Preturi: ";
			for (int i = 0; i < this->nrCarti; i++) {
				cout << this->vectorPreturi[i] << " ";
			}
		}
	}
};

int Librarie::nrLibrarii = 0;

int main() {
	Librarie l1;
	l1.afisare();

	float* preturi = new float[2] { 25.5f, 40.0f };
	Librarie* l2 = new Librarie(5, "Humanitas", 2, preturi);
	l2->afisare();

	Librarie l3 = *l2;
	l3.afisare();

	delete[] preturi;
	delete l2;

	cout << "\nTotal librarii: " << Librarie::nrLibrarii << endl;
	return 0;
}
