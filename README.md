# -
#include<stdio.h>
#include<stdlib.h>
#include<iostream>
#include<fstream>

using namespace std;
sad
cdd

asd

da
struct base{
	int num;
	float latitude;
	float longtitude;
	double kdt;
};
typedef struct base node;

node d[1033];

int part(int low,int high);
void equal(node &a,node &b);

node rSort(int k,int low,int high){
	
	int m,n;
	int find=0;
	
	if(low==high){
		return d[high];
	} 	
	else{		
		if(low<high){
			
			m=part(low,high);
			n=m-low+1;
			if(k<n){
				return rSort(k,low,m);
			}
			else if(k==n){
				return d[m];
			} 
			else{
				return rSort(k-n,m+1,high);
			}
		}
	}
}

int part(int low,int high){
	int i=low;
	int j=high+1;
	node temp;
	node ex;
	equal(ex,d[low]);
	//cout << "2"<< endl;
	while(true){	
		while((d[++i].kdt-ex.kdt<=0)&&i<high){
			//i++;
		}
		while((d[--j].kdt-ex.kdt>0)){
			//j--;
		}
		if(i>=j){
			break;
		}
		equal(temp,d[j]);
		equal(d[j],d[i]);
		equal(d[i],temp);
	}
	
	equal(d[low],d[j]);
	equal(d[j],ex);
	return j;
	
}

void equal(node &a,node &b){
	a.kdt=b.kdt;
	a.latitude=b.latitude;
	a.longtitude=b.longtitude;
	a.num=b.num;
	//cout<<a.kdt<<" "<<b.kdt<<endl;
}


int main(){
	int i=0;
	float min,max,fifth,fiftith; 
	FILE* infile=fopen("data.txt","r");
	if(infile==NULL){
		cout << "打开失败"<< endl;
	}
	while(!feof(infile)){
		fscanf(infile,"%d,%f,%f,%lf\n",&d[i].num,&d[i].longtitude,&d[i].latitude,&d[i].kdt);
		//cout << d_base[i].num <<" "<<d_base[i].longtitude<<" "<<d_base[i].latitude<<" "<<d_base[i].kdt<< endl;
		i++;
	}
	min=rSort(1,0,1032).kdt;
	fifth=rSort(5,0,1032).kdt;
	fiftith=rSort(50,0,1032).kdt;
	max=rSort(1033,0,1032).kdt;
	
	cout<<min<<endl;
	cout<<fifth<<endl;
	cout<<fiftith<<endl;
	cout<<max<<endl;
	
	/*for(i=0;i<=1032;i++){
		cout << d[i].num <<" "<<d[i].longtitude<<" "<<d[i].latitude<<" "<<d[i].kdt<< endl;
	}*/
	return 0;
}
