RAD
===
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <locale.h>

int main()
{
    setlocale( LC_ALL,"Russian" );
    int const N=200;
    char array[N];
    int countWords=0;
    int countSentence=0;
    int countSpeech=0;
    char word;
    FILE *VicHugo;
    VicHugo=fopen("Hugo.txt","r");
    if (VicHugo == NULL)
    {
        perror("Error opening file");
    }
    else
    {
        while (!feof(VicHugo))
        {
            if (fgets(array, N-1, VicHugo) != NULL)
            {
                countWords++;
                for (int i=0; i<=strlen(array); i++)
                {
                    if ((array[i]==' ') && (array[i+1]!=' '))
                    {
                        countWords++;
                    }
                    if ((array[i]=='.')&&(array[i+1]!='.'))
                    {
                        countSentence++;
                    }
                    if ((array[i]=='.')&&(array[i-1]=='M'))
                    {
                        countSentence--;
                    }
                    if (array[i]=='"')
                    {
                        countSpeech++;
                    }
                }
            }
        }
    }
    if ( fclose (VicHugo) == EOF)
    {
        printf("error closing file");
        return -1;
    }

    fclose(VicHugo);
    printf("Всего слов:        %d\nВсего предложений: %d\nВсего выражений    %d\n\n\n",countWords,countSentence,countSpeech/2);

    return 0;
}
