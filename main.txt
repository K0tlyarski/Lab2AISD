#include <iostream>
#include "Header.h"
#include <cmath>

void GetValueFromUser(int& value)
{
    while (true)
    {
        std::cin >> value;
        if (std::cin.fail() || std::cin.bad())
        {
            std::cin.clear();
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
            std::cout << "The input is incorrect, please try again" << std::endl;
        }
        else
        {
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
            return;
        }
    }
}

void GetFloatValueFromUser(float& value)
{
    while (true)
    {
        std::cin >> value;
        if (std::cin.fail() || std::cin.bad())
        {
            std::cin.clear();
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
            std::cout << "The input is incorrect, please try again" << std::endl;
        }
        else
        {
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
            return;
        }
    }
}


bool IsValueInRange(const int& value, const float& left_border, const float& right_border)
{
    return (value >= left_border && value <= right_border);
}

void GetValueFromUserInRange(int& value, const float& left_border, const float& right_border, const char* condition = "")
{
    std::cout << condition;
    while (true)
    {
        GetValueFromUser(value);
        if (IsValueInRange(value, left_border, right_border))
        {
            return;
        }
        else
        {
            std::cout << "The value is not in range, try again" << std::endl;
        }
    }
}
void MenuWorkingWithVector(Vector& vector)
{
    bool working_with_vector = true;
    while (working_with_vector)
    {
        
        std::cout << vector << std::endl;
        std::cout << "You are now editing the first vector, Enter:" << std::endl;
        std::cout << "0 - Changing an element by index\n1 - Adding elements to a vector" << std::endl;
        std::cout << "2 - Dividing a vector by a number\n3 - Vector multiplication by a number " << std::endl;
        std::cout << "4 - Deleting an element by index\n5 - Finding the perpendicular" << std::endl;
        std::cout << "6 - Adding an element to the end of a vector\n7 - Inserting an element by index" << std::endl;
        std::cout << "8 - Output of an element by index\n9 - Finish working with the vector" << std::endl;
        int editing_vector = 0;
        GetValueFromUserInRange(editing_vector, (int)0, (int)9, "Enter the number in range[0;9] ");
        switch (editing_vector)
        {
            case (0):
            {
                if (vector.GetSize())
                {
                    try {
                        std::cout << "Enter a index of element to edit" << std::endl;
                        int index = 0;
                        GetValueFromUserInRange(index,0,vector.GetSize());
                    
                        std::cout << "Enter a new value for the element" << std::endl;
                        float value = 0;
                        GetFloatValueFromUser(value);
                        vector[index] = value;
                    }
                    catch (std::out_of_range& ex)
                    {
                        std::cout << ex.what() << " Try again" << std::endl;
                        
                    }
                }
                break;
            }
            case (1):
            {
                std::cout << "\n\n\n\n\n\n\n\n\n\n\n\n" << std::endl;
                //std::cout << "Enter a scalar" << std::endl;
                int count;
                float n;
                std::cout<<"Enter the vector length"<<std::endl;
                std::cin>>count;
                for (int i = 0; i<count; i++) {
                    std::cin>>n;
                    vector.PushBack(n);
                }
                /*bool flag = true;
                float n;
                while (flag == true) {
                    std::cin>>n;
                    if (n ==0) {
                        flag = false;
                    }
                    vector.PushBack(n);
                }*/
                break;
            }
            case (2):
            {
                std::cout << "Enter a scalar" << std::endl;
                int scalar = 0;
                GetValueFromUser(scalar);
                try
                {
                    vector /= scalar;
                }
                catch (const char* ex)
                {
                    std::cout << ex << " Try again" << std::endl;
                    
                }
                break;
            }
            case (3):
            {
                /*std::cout << "Enter a scalar" << std::endl;
                int scalar = 0;
                GetValueFromUser(scalar);
                vector *= scalar;*/
                Vector vector2;
                std::cout << "Enter a scalar" << std::endl;
                int scalar = 0;
                GetValueFromUser(scalar);
                vector2 = scalar * vector;
                std::cout<<vector2<<std::endl;
                
                break;
                break;
            }
            case (4):
            {
                if (vector.GetSize())
                {
                    
                    std::cout << "Enter the index of element to delete" << std::endl;
                    int index = 0;
                    GetValueFromUser(index);
                    try
                    {
                        vector.Erase(index);
                    }
                    catch (std::out_of_range& ex)
                    {
                        std::cout << ex.what() << " Try again" << std::endl;
                        
                    }
                }
                else
                {
                    std::cout << "There are no elements to delete" << std::endl;
                }
                    
                break;
            }
            case (5):
            {
                Vector vector2;
                float intermediate_result;
                float result_1;
                for (int i = 0; i<vector.GetSize(); i++) {
                    vector2.PushBack(1);
                }
                
                for (int i = 0; i<vector.GetSize(); i++) {
                    
                    intermediate_result = -(vector.operator[](i) * vector2.operator[](i));
                    result_1 = intermediate_result / vector.operator[](0);
                }
                
                vector2.Insert(result_1, 0);
                vector2.Erase(vector2.GetSize()-1);
                
                float sqr;
                for (int i = 0; i<vector2.GetSize(); i++) {
                    float inc;
                    inc += vector2.operator[](i)*vector2.operator[](i);
                    sqr = sqrt(inc);
                    
                }
                Vector vector3;
                for (int i = 0; i<vector2.GetSize(); i++) {
                    vector3.PushBack(vector2.operator[](i)/sqr);
                }
                std::cout<<"Perpendicular vector: ";
                vector3.Print();
                std::cout<<"\n\n\n";
                break;
            }
            case (6):
            {
                float number;
                std::cout<<"Enter the element: ";
                GetFloatValueFromUser(number);
                vector.PushBack(number);
                break;
            }
            case (7):
            {
                try {
                    std::cout<<"Enter the element: ";
                    float InsertNumber;
                    GetFloatValueFromUser(InsertNumber);
                    std::cout<<"Enter the index: ";
                    int InsertIndex;
                    GetValueFromUserInRange(InsertIndex,0,vector.GetSize());
                    vector.Insert(InsertNumber, InsertIndex);
                } catch (std::out_of_range& ex) {
                    std::cout << ex.what() << " Try again" << std::endl;
                }
                break;
                
                
            }
            case (8):
            {
                try {
                    std::cout<<"Enter the index: ";
                    int index;
                    GetValueFromUserInRange(index,0,vector.GetSize());
                    std::cout<<vector.operator[](index)<<std::endl;
                    
                } catch (std::out_of_range& ex) {
                    std::cout << ex.what() << " Try again" << std::endl;
                }
                break;
            }
            case (9)://finish working
            {
                working_with_vector = false;
                break;
            }
                
        }
    }
}


void Menu(float)
{
    bool function_is_working = true;
    Vector first_vector;
    Vector second_vector;
    while (function_is_working)
    {
        std::cout << "First vector:" << first_vector << std::endl;
        std::cout << "\nSecond vector:" << second_vector << std::endl;
        std::cout << "Enter:\n0 - to work and edit with single vector" << std::endl;
        std::cout << "1 - to sum two vectors\n2 - to substract second vector from first" << std::endl;
        std::cout << "3 - to calculate the scalar product of two vectors\n4 - clear two vectors" << std::endl;
        std::cout << "5 - Print are two vectors equal or not\n6 - make first vector equal to second\n";
        std::cout << "7 - finish working with vectors" << std::endl;
        int action = 0;
        GetValueFromUserInRange(action, (long int)0, (long int)7, "\nEnter a number in range [0;7]");
        switch (action)
        {
        case (0):
        {
            int order_number = 0;
            GetValueFromUserInRange(order_number, (long int)1, (long int)2, "Enter the order number of vector you wanted to edit");
            
            if (order_number == 1)
            {
                MenuWorkingWithVector(first_vector);
            }
            else
            {
                MenuWorkingWithVector(second_vector);
            }
            break;
        }
        case (1):
        {
            try
            {
                Vector sum = first_vector + second_vector;
                std::cout << sum;
            }
            catch (const char* ex)
            {
                std::cout << ex << std::endl;
            }
            
            break;
        }
        case (2):
        {
            try
            {
                Vector subtraction = first_vector - second_vector;
                std::cout << subtraction;
            }
            catch (const char* ex)
            {
                std::cout << ex << std::endl;
            }
            
            break;
        }
        case (3):
        {
            try
            {
                float scalar_product = first_vector.DotProduct(second_vector);
                std::cout << scalar_product << std::endl;
            }
            catch (const char* ex)
            {
                std::cout << ex << std::endl;
            }
            
            break;
        }
        case (4):
        {
            first_vector.Clear();
            second_vector.Clear();
            break;
        }
        case (5):
        {
            first_vector == second_vector ? std::cout << "Vectors are equal" << std::endl :
                std::cout << "Vectors are different" << std::endl;
            
            break;
        }
        case (6):
        {
            first_vector = second_vector;
            break;
        }
        case (7):
        {
            function_is_working = false;
            break;
        }

        }
        
    }
}






int main()
{
    bool working_with_vectors = true;
    Menu((float)0.0);
}


