#include <iostream>

class Car
{
    public:
    float Kecepatan = 10;
    float Bensin = 100;
    float Bensin_max = 100;
    int penumpang = 4;
    
    virtual void jalan()
    {
        Bensin -= Kecepatan;
        std::cout << "Mobil ini berjalan sejauh " << Kecepatan << " km/jam" << std::endl;
    }
};

class SuperCar : public Car
{
    public:
    SuperCar() {
        Kecepatan = 100;
        Bensin = 1000;
        Bensin_max = 1000;
    }
    
    SuperCar(float _Kecepatan, float _Bensin, float _Bensin_max)
    {
        Kecepatan = _Kecepatan;
        Bensin_max = _Bensin_max;
        Bensin = _Bensin;
    }
};

class Pickup : public Car
{
    public:
    int kapasitas = 1;
    int kapasitas_max = 100;
    
    void angkut(int berat_barang)
    {
        if(kapasitas + berat_barang <= kapasitas_max)
        {
            kapasitas += berat_barang;
            Kecepatan = Kecepatan / kapasitas;
            std::cout << "Barang berhasil ditambahkan!" << std::endl;
        }
        else
        {
            std::cout << "Barang tidak dapat ditambahkan!" << std::endl;
        }
    }
    
    void jalan() override {
        Bensin -= Kecepatan * kapasitas + kapasitas;
        std::cout << "Mobil ini berjalan sejauh " << Kecepatan << " km/jam dengan kapasitas terpakai " << kapasitas << " kg" << std::endl;
    }
};

int main()
{
    SuperCar ferrari;
    SuperCar superFerrari(9999, 9999, 9999);
    Pickup truckKun;
    
    ferrari.jalan();
    ferrari.jalan();
    
    superFerrari.jalan();
    superFerrari.jalan();
    
    truckKun.jalan();
    truckKun.angkut(90);
    truckKun.angkut(100);
    truckKun.jalan();

    return 0;
}

// Furina best girl