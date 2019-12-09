#include <iostream>
#include <vector>
#include <time.h>
#include <windows.h>
#include <algorithm>
#include <random>
#include <iomanip>
#include <chrono>
using namespace std;

void MakeList(vector <int>& data, long long num);
void Display(vector <int> data);
long long SequentialSearch(vector <int>& data, int key);
void FirstSorting(vector <int>& data, long long key, long long& pos);
void SecondSorting(vector <int>& data, long long key, long long& pos);
long long InterpolationSearch(vector <int>& data, int key);
default_random_engine rng{ random_device{}() };
int main()
{
	srand(time(NULL));
	clock_t t = 0;
	vector <int> data;
	double time_taken = 0;
	long long pos;
	char choice;
	int key;
	cout << "Iveskite kiek duomenu planuojate rusiuoti: " << endl;
	long long num;
	cin >> num;
	data.reserve(num);
	cout << "Sudaromas duomenu sarasas..." << endl;
	Sleep(500);
	MakeList(data, num);
	cout << "Rusiuojamas duomenu sarasas...\n";
	Sleep(500);
	sort(data.begin(), data.end());
	while (true)
	{
		cout << "Pasirinkite kuri atveji tikrinti: \n";
		cout << "1. Worst case, elementas, kuri reikia rasti, yra saraso gale\n";
		cout << "2. Average case, elementas, kuri reikia rasti, yra saraso viduryje\n";
		cout << "3. Pasirinkti elementa paciam.\n";
		cin >> choice;
		if (choice == '1' || choice == '2' || choice == '3')
			break;
	}
	switch (choice)
	{
	case '1':
		key = data[data.size() - 1];
		break;
	case '2':
		key = data[(data.size() - 1) / 2];
		break;
	case '3':
		cout << "Iveskite skaiciu, kuri norite rasti duomenu sarase: ";
		cin >> key;
		break;
	default:
		cout << "Fatal error.\n";
		break;
	}
	cout << "\nIeskoma rusiuotame sarase Nuosekliu paieskos algoritmu.";
	FirstSorting(data, key, pos);
	cout << "Ieskoma rusiuotame sarase Interpoliaciniu paieskos algoritmu.\n";
	SecondSorting(data, key, pos);
	return 0;
}

void Display(vector <int> data)
{
	for (auto i : data)
		cout << i << " ";
	cout << endl;
}

void MakeList(vector <int> &data, long long num)
{
	data.erase(data.begin(), data.end());
	for (long long i = 0; i < num; i++)
	{
		data.push_back(i);
	}
	shuffle(data.begin(), data.end(), rng);
}

long long SequentialSearch(vector <int>& data, int key)
{
	for (long long i = 0; i < data.size(); i++)
	{
		if (data[i] == key)
			return i;
	}
	return -1;
}

void FirstSorting(vector <int>& data, long long key, long long &pos)
{
	chrono::high_resolution_clock::time_point t1 = chrono::high_resolution_clock::now();
	pos = SequentialSearch(data, key);
	chrono::high_resolution_clock::time_point t2 = chrono::high_resolution_clock::now();
	chrono::duration<double> time_span = chrono::duration_cast<chrono::duration<double>>(t2 - t1);
	if (pos != -1)
		cout << "\nElementas rastas! Paieska uztruko " << fixed << setprecision(10) << time_span.count() << " sekundes. Jo pozicija duomenu sarase: " << pos + 1 << endl;
	else cout << "Toks elementas nerastas.\n";
}

void SecondSorting(vector <int>& data, long long key, long long& pos)
{
	chrono::high_resolution_clock::time_point t1 = chrono::high_resolution_clock::now();
	pos = InterpolationSearch(data, key);
	chrono::high_resolution_clock::time_point t2 = chrono::high_resolution_clock::now();
	chrono::duration<double> time_span = chrono::duration_cast<chrono::duration<double>>(t2 - t1);
	if (pos != -1)
		cout << "Elementas rastas! Paieska uztruko " << fixed << setprecision(10) << time_span.count() << " sekundes. Jo pozicija duomenu sarase: " << pos + 1 << endl;
	else cout << "Toks elementas nerastas.\n";
}

long long InterpolationSearch(vector <int>& data, int key)
{
	long long low, high, pos;
	low = 0;
	high = data.size() - 1;
	while (low <= high && key >= data[low] && key <= data[high])
	{
		if (low == high)
		{
			if (data[low] == key)
				return low;
			else return -1;
		}
		pos = (((double)(high - low) / (data[high] - data[low])) * (key - data[low]));
		if (data[pos] == key)
			return pos;
		if (data[pos] < key)
			low = pos + 1;
		else high = pos - 1;
	}
	return -1;
}
