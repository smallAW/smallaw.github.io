---
title : 高精度模板
---
做高精度的题好烦啊!!!!
```cpp
#include <iostream>
#include <string>
using namespace std;

struct Bignum
{
private:
    Bignum jian(Bignum b)
    {
        Bignum a = *this;
        Bignum c;
        for (int i = 1; i <= this->num[0]; i++)
        {
            if (a.num[i] < b.num[i])
            {
                a.num[i] += 10;
                a.num[i + 1]--;
            }
            c.num[i] = a.num[i] - b.num[i];
        }
        int lenc = a.num[0];
        while (c.num[lenc] == 0 && lenc > 1)
            lenc--;
        c.num[0] = lenc;
        return c;
    }

public:
    int num[2005]{0};
    friend ostream &operator<<(ostream &out, Bignum a)
    {
        for (int i = a.num[0]; i >= 1; i--)
            printf("%d", a.num[i]);
        return out;
    }
    friend istream &operator>>(istream &in, Bignum &a)
    {
        string s;
        in >> s;
        a.num[0] = s.size();
        for (int i = 1; i <= a.num[0]; i++)
            a.num[i] = s[a.num[0] - i] - '0';
        return in;
    }
    bool operator==(Bignum b)
    {
        if (this->num[0] != b.num[0])
            return 0;
        for (int i = this->num[0]; i > 0; i--)
            if (this->num[i] != b.num[i])
                return 0;
        return 1;
    }
    bool operator>(Bignum b)
    {
        if (this->num[0] > b.num[0])
            return 1;
        if (this->num[0] < b.num[0])
            return 0;
        for (int i = this->num[0]; i > 0; i--)
        {
            if (this->num[i] > b.num[i])
                return 1;
            if (this->num[i] < b.num[i])
                return 0;
        }
        return 0;
    }
    bool operator>=(Bignum b)
    {
        if (this->num[0] > b.num[0])
            return 1;
        if (this->num[0] < b.num[0])
            return 0;
        for (int i = this->num[0]; i > 0; i--)
        {
            if (this->num[i] > b.num[i])
                return 1;
            if (this->num[i] < b.num[i])
                return 0;
        }
        return 1;
    }
    bool operator<(Bignum b)
    {
        if (this->num[0] > b.num[0])
            return 0;
        if (this->num[0] < b.num[0])
            return 1;
        for (int i = this->num[0]; i > 0; i--)
        {
            if (this->num[i] > b.num[i])
                return 0;
            if (this->num[i] < b.num[i])
                return 1;
        }
        return 0;
    }
    bool operator<=(Bignum b)
    {
        if (this->num[0] > b.num[0])
            return 0;
        if (this->num[0] < b.num[0])
            return 1;
        for (int i = this->num[0]; i > 0; i--)
        {
            if (this->num[i] > b.num[i])
                return 0;
            if (this->num[i] < b.num[i])
                return 1;
        }
        return 1;
    }
    Bignum operator+(Bignum b)
    {
        Bignum c;
        int lenc = 1;
        int x = 0;
        while (lenc <= this->num[0] || lenc <= b.num[0])
        {
            c.num[lenc] = this->num[lenc] + b.num[lenc] + x;
            x = c.num[lenc] / 10;
            c.num[lenc] %= 10;
            lenc++;
        }
        if (x != 0)
            c.num[lenc] = x;
        else
            lenc--;
        c.num[0] = lenc;
        return c;
    }
    Bignum operator-(Bignum b)
    {
        Bignum c;
        if (*this < b)
        {
            c = b.jian(*this);
            return c;
        }
        else
        {
            c = this->jian(b);
            return c;
        }
    }
    Bignum operator*(Bignum b)
    {
        Bignum a = *this;
        Bignum c;
        for (int i = 1; i <= b.num[0]; i++)
        {
            for (int j = 1; j <= a.num[0]; j++)
                c.num[i + j - 1] += b.num[i] * a.num[j];
        }
        int lenc = a.num[0] + b.num[0];
        int x = 0;
        for (int i = 1; i <= lenc; i++)
        {
            c.num[i] += x;
            x = c.num[i] / 10;
            c.num[i] %= 10;
        }
        while (c.num[lenc] == 0 && lenc > 1)
            lenc--;
        c.num[0] = lenc;
        return c;
    }
    Bignum operator/(long long b)
    {
        Bignum c;
        Bignum a = *this;
        long long x = 0;
        for (int i = a.num[0]; i >= 1; i--)
        {
            x = x * 10 + a.num[i];
            c.num[i] = x / b;
            x = x % b;
        }
        int lenc = a.num[0];
        while (c.num[lenc] == 0 && lenc > 1)
            lenc--;
        c.num[0] = lenc;
        return c;
    }
    Bignum operator/(Bignum b)
    {
        Bignum c, ta;
        for (int i = 0; i <= num[0]; i++)
            ta.num[i] = num[i];
        c.num[0] = ta.num[0] - b.num[0] + 1;
        int awa = ta.num[0] - b.num[0];
        for (int i = ta.num[0]; i >= 1; i--)
        {
            if (i > awa)
                b.num[i] = b.num[i - awa];
            else
                b.num[i] = 0;
        }
        b.num[0] = ta.num[0];
        for (int i = c.num[0]; i >= 1; i--)
        {
            while (ta >= b)
            {
                ta = ta - b;
                c.num[i]++;
            }
            for (int i = 1; i < b.num[0]; i++)
                b.num[i] = b.num[i + 1];
            b.num[b.num[0]] = 0;
            b.num[0]--;
        }
        while (c.num[c.num[0]] == 0 && c.num[0] > 1)
            c.num[0]--;
        return c;
    }
    long long operator%(long long b)
    {
        Bignum c;
        Bignum a = *this;
        long long x = 0;
        for (int i = a.num[0]; i >= 1; i--)
        {
            x = x * 10 + a.num[i];
            c.num[i] = x / b;
            x = x % b;
        }
        int lenc = a.num[0];
        while (c.num[lenc] == 0 && lenc > 1)
            lenc--;
        c.num[0] = lenc;
        if (x == 0)
            return b;
        else
            return x;
    }
    void operator=(long long b)
    {
        if (b == 0)
        {
            num[0] = 1;
            num[1] = 0;
            return;
        }
        long long awa = b, len = 0;
        while (awa)
        {
            num[++len] = awa % 10;
            awa /= 10;
        }
        num[0] = len;
    }
    void operator+=(Bignum b)
    {
        *this = *this + b;
    }
    void operator-=(Bignum b)
    {
        *this = *this - b;
    }
    void operator*=(Bignum b)
    {
        *this = *this * b;
    }
    void operator/=(long long b)
    {
        *this = *this / b;
    }
    void operator/=(Bignum b)
    {
        *this = *this / b;
    }
};
Bignum a, b;
int main()
{
    cin >> a >> b;
    cout << a + b << a - b << ' ' << a - b << " " << a / b  << ' ';
    return 0;
}
```