# lab3pt1
//  Monica Andrade
//  Comp 322
//  Lab3pt1
//  File Permissions and Directory Info
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
    uid_t uid;
    gid_t gid;
    
    int status = 0;
    
    struct stat buf;
    
    int i;
    
    for(i = 1; i <argc; i++)
    {
        pid = fork();
        stat(argv[i], &buf);
       

        
        if(pid == 0)
        {
            uid = getuid();
            gid = getgid();
            
            printf("Filename: %s\tPID: %d\n", argv[i], getpid());
            
            if(buf.st_uid == uid)
            {
                
                printf("You have owner permission:");
                if(buf.st_mode & S_IRUSR)
                {
                    printf("read");
                }
                if(buf.st_mode & S_IWUSR)
                {
                    printf("write");
                }
                if(buf.st_mode & S_IXUSR)
                {
                    printf("excute");
                }
                 printf("\n\n");
            }
            else if(buf.st_gid == gid)
            {
                printf("You have group permisson:");
                if(buf.st_mode & S_IRGRP)
                {
                    printf("read");
                }
                if(buf.st_mode & S_IWGRP)
                {
                    printf("write");
                }
                if(buf.st_mode & S_IXGRP)
                {
                    printf("excute");
                }
                 printf("\n\n");
            }
            else
            {
                printf("You have general permission:");
                if(buf.st_mode & S_IROTH)
                {
                    printf("read");
                }
                if(buf.st_mode & S_IWOTH)
                {
                    printf("write");
                }
                if(buf.st_mode && S_IXOTH)
                {
                    printf("execute");
                }
                printf("\n\n");
            }
           
            exit(1);
        }
        
        }
        if(pid > 0){
             for(int i = 1; i <argc; i++){
            pid = wait(&status);
        }
        printf("\n\n");
        
    }
    }
    system("ps -H");
    printf("Done!\n");
    
    return 0;
}
