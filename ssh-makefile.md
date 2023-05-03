# SSH-Makefile (Remote Compilation)

## Installation

![image](https://user-images.githubusercontent.com/33444140/235699865-be823361-ae80-4d64-a900-ccb143a1ccfd.png)

If ssh was inactive. Start the ssh service

![image](https://user-images.githubusercontent.com/33444140/235725436-51ce5578-daab-4aa7-a109-df5773f2d327.png)

![image](https://user-images.githubusercontent.com/33444140/235700017-cda553c9-92e8-4b6c-ad39-abb6cc535001.png)

![image](https://user-images.githubusercontent.com/33444140/235699678-3d45ed4e-9268-438e-9729-28c20b16f44f.png)

## Key-Based Authentication
Leave the filename part blank to save the key in default file `id_rsa`

![image](https://user-images.githubusercontent.com/33444140/235738652-2c159682-9991-4c27-9425-f3208d426ffe.png)

![image](https://user-images.githubusercontent.com/33444140/235738822-003c76ea-c00e-4cbd-86a9-007ecf9c8e60.png)

![image](https://user-images.githubusercontent.com/33444140/235738924-89da3b58-9631-4bac-90aa-fd727d3e4c4f.png)

## Makefile                                        
    REMOTE_SERVER = tousif@192.168.59.130
    SRC_DIR = /home/tousif/sshmakeprog
    CC = gcc

    .PHONY: all clean

    all: program remote run-remote

    program: prog1 prog2
            $(CC) prog1.c -o prog1
            $(CC) prog2.c -o prog2

    remote: prog1 prog2
            scp prog1 prog2 $(REMOTE_SERVER):$(SRC_DIR)

    run-remote: remote
            ssh $(REMOTE_SERVER) 'cd $(SRC_DIR) && ./prog1'
            ssh $(REMOTE_SERVER) 'cd $(SRC_DIR) && ./prog2'

    clean:
            rm -f program

## Makefile O/p

![image](https://user-images.githubusercontent.com/33444140/235840325-a7ae1fa8-a3d4-4317-8cd7-8c7e45822d18.png)
