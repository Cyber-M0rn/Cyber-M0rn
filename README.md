#include<iostream>
#include<math.h>       // used for pow() function. pow() function is used to calculate some power of a number
using namespace std;

int find_determinant(int matrix[3][3], int n)
{
    int a,b,c,d,i,j,k;
    int temp_determinant=0,subcofactor_matrix[3][3],cofactor_i,cofactor_j;
    
    if(n==1)          // if order of a matrix is 1
        return matrix[0][0];
    
    if(n==2)         // if order of a matrix is 2
    {
       a=matrix[0][0];
       b=matrix[0][1];
       c=matrix[1][0];
       d=matrix[1][1];
       
       return (a*d - b*c);
    }
    
    if(n==3)        // if order of a matrix is 3
    {
        // loop for 0th row elements. Because for finding determinant of a matrix we only need to find out cofactors of 0th row elements
        for(k=0; k<n; k++) 
        {
            cofactor_i = 0;

                //Here, we have started loop from 1. Because we don't want to consider elements of same row for finding cofactor of an element
            for (i=1; i<n; i++) 
            {
               cofactor_j = 0;
               for (j=0; j<n; j++) 
                {
                    if (j!=k)  // we have used this codition. because we don't want to consider elements of same column for finding cofactor of an element
                    {
                        //forming sub_cofactor matrix
                        subcofactor_matrix[cofactor_i][cofactor_j] = matrix[i][j];
                        cofactor_j++;                        
                    }

                }
                cofactor_i++;
            }
            
            // calculating determinant of a matrix
            temp_determinant = temp_determinant + (pow(-1, k) * matrix[0][k] * find_determinant( subcofactor_matrix, n - 1 ));
        }
    }
    return temp_determinant;
}


int main()
{
    int i,j,n,determinant,matrix[3][3];
    
    cout<<"Enter order of a matrix (1/2/3): ";
    cin>>n;
    while( n<1 || n>3 )            // if mentioned order is not in between 1 and 3
    {
        cout<<"\nPlease..Enter order of a matrix in 1 to 3: ";
        cin>>n;
    }
    
    cout<<"\nEnter the elements of a matrix: ";       // Taking elements of matrix as a input
    for(i=0; i<n; i++)
        for(j=0; j<n; j++)
            cin>>matrix[i][j];
    
    cout<<"\nEntered matrix:\n";        // Displaying entered matrix
    for(i=0; i<n; i++)
    {
        for(j=0; j<n; j++)
        {
            cout<<matrix[i][j]<<" ";
        }
        cout<<"\n";
    }
            
    determinant=find_determinant(matrix,n);     // function call to find_determinant
    cout<<"\nDeterminant of the Entered matrix is: "<<determinant;
    return 0;
}
