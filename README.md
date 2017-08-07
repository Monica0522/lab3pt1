# lab3pt1
//  Monica Andrade
//  Comp 322
//  Lab3pt1
//
//  Created by Monica Andrade on 8/3/17.
//  Copyright © 2017 Monica Andrade. All rights reserved.
//

#include <unistd.h>
#include <sys/types.h>
#include <string.h>
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <sys/wait.h>

int main(int argc, const char * argv[]) {
    
    pid_t pid;
    int i;
    
    for(i = 1; i <argc; i++)
    {
        pid = fork();
        
        if(pid > 0)
        {
            printf("Filename: %s\tPID: %d\n", argv[i], getpid());
            exit(1);
        }
        else if (pid ==0){
            printf("Filename: %s\tPID: %d\n", argv[i], getpid());
            exit(1);
        }
        else
        {
            wait(NULL);
        }
    }
    system("ps -H");
    printf("Done!\n");
    
    return 0;
