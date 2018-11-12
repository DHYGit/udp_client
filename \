#include <stdio.h>
#include <string.h>
#include <errno.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

int main(){
	int sock = socket(AF_INET, SOCK_DGRAM, 0);
	if(sock < 0){
		printf("create socket failed \n");
		exit(1);
	}
	struct sockaddr_in addr_serv;
	int len;
	memset(&addr_serv, 0, sizeof(addr_serv));
	addr_serv.sin_family = AF_INET;
	addr_serv.sin_addr.s_addr = inet_addr("127.0.0.1");
	addr_serv.sin_port = htons(8000);
	len = sizeof(addr_serv);

	int send_num;
	int recv_num;
	char send_buf[2000] = {0};
	char recv_buf[2000] = {0};
	while(fgets(send_buf, sizeof(send_buf), stdin) != NULL){
		send_num = sendto(sock, send_buf, strlen(send_buf), 0, (struct sockaddr*)&addr_serv, len);
		if(send_num < 0){
			printf("sendto error\n");
			exit(1);
		}
		recv_num = recvfrom(sock, recv_buf, sizeof(recv_buf), 0, (struct sockaddr*)&addr_serv, (socklen_t*)&len);
		recv_buf[recv_num] = '\0';
		printf("client receive %d bytes:%s\n", recv_num, recv_buf);
	}
	close(sock);
	return 0;
}
