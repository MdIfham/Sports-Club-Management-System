#include<fstream.h>
#include<conio.h>
#include<stdio.h>
#include<string.h>
#include<dos.h>

void facd();          //facility deatails
int facin(int fc);    //to input fcility codes for a member

struct Dt
{ int dd,mm,yy;};

int isleap(int year)        //to check leap year
 { return (((year%4==0)&&(year%100!=0)||(year%400)==0)); }

  int valid_Dt(Dt du)                //to validate date
 {  int ymax=2025,ymin=1990;
    int d=du.dd,m=du.mm,y=du.yy;
     if(y>ymax||y<ymin)   return 0;
     if(m<1||m>12)        return 0;
     if(d<1||d>31)        return 0;
 if(m==2)
   { if(isleap(y))
	 { if(d<1||d>29)  return 0; }
   else if(d<1||d>28)  return 0;}
   else if(m==4||m==6||m==9||m==11)
	    if(d<1||d>30)
	     return 0;
       return 1;   }

       void inDt(Dt &du)                          //to input date
{ x:  cin>>du.dd>>du.mm>>du.yy;
      if(valid_Dt(du));
      else { cout<<"Enter valid date:";   goto x;   } }

 int Dtcmp(Dt d1,Dt d2)       //to compare date
 {    if(d1.yy<d2.yy)
	  return 10;                       //valid
      else if(d1.yy==d2.yy)
	   { if(d1.mm<d2.mm)
	     return 10;                    //valid
	     else if(d1.mm==d2.mm)
		   {if(d1.dd<d2.dd)
			return 10;
		     else if(d1.dd==d2.dd)
			return 1;            //valid date equal
		     else if(d1.dd>d2.dd)
			return 0;}
	      else if(d1.mm>d2.mm)
			 return 0;  }

	    else if(d1.yy>d2.yy)
		   return 0;

	  return 0;  }


class faci
{  int fc;
   public:
   char fac[100];
   void in(int cd)
  {    fc=cd;
     cout<<"Facility code:"<<fc<<' ';
     cout<<"Enter facility:";          gets(fac); }
   void out()
   { cout<<"Facility code:"<<fc;
     cout<<" Facility:"<<fac<<endl; }

 int ret_fc(){ return fc;} }fa;

class fees
{ int mco;
  Dt dos;
  public:
  float amount;
  void in(int cd)
{   mco=cd;
   cout<<"Member code:"<<mco<<' ';
   cout<<"Enter date of submission(dd/mm/yyyy):";   inDt(dos);
   cout<<"Enter amount:";    cin>>amount;}
 void out()
{  cout<<"Member code:"<<mco<<endl;
   cout<<"Date of submission:";
   cout<<dos.dd<<' '<<dos.mm<<' '<<dos.yy<<endl;
   cout<<"Amount:"<<amount;  }

int ret_mcode()   {return mco;}
Dt ret_dos()    {return dos;}         }fe;


class memb
{ int mco;
  public:
  int fc1,fc2,fc3,noch;
  char mna[100],ads[100],phno[100];
  Dt doj;
  void in(int code,int choice);
  void out()
   { cout<<"Member code:"<<mco<<'\n';
     cout<<"Member name:"<<mna<<'\n';
     cout<<"Date of joining:";
     cout<<doj.dd<<' '<<doj.mm<<' '<<doj.yy<<'\n';
     cout<<"Address:"<<ads<<'\n';
     cout<<"Phone no:"<<phno<<'\n';
     cout<<"Facility code 1:"<<fc1<<'\n';
     cout<<"Facility code 2:"<<fc2<<'\n';
     cout<<"Facility code 3:"<<fc3<<'\n';
     cout<<"No of children:"<<noch<<'\n';   }

     int ret_mco() { return mco;}    }m;

  void memb::in(int code,int ch=0)
   { int t;
     mco=code;
     cout<<"Member code:"<<mco;
     cout<<"\nEnter member name:";     gets(mna);
 re: cout<<"Enter date of joining (dd/mm/yyyy):";  inDt(doj);
     if(ch==1)
     {  Dt d=fe.ret_dos();
	if(Dtcmp(doj,d));
	else { cout<<"Enter Valid date ofjoining as before "
		    <<"Date of fee submission i.e.:"
		    <<d.dd<<' '<<d.mm<<' '<<d.yy<<'\n';
		    goto re;}     }

     cout<<"Enter Address:";           gets(ads);
     cout<<"Enter Phone no:";          gets(phno);
     facd();
     for(int i=1;i<=3;++i)
  {   cout<<"Enter facility code "<<i<<':';   cin>>t;
      if(facin(t))
     {  if(i==1)
	fc1=t;
       else if(i==2)
	fc2=t;
       else if(i==3)
	fc3=t;        }
	else i--;    }

     cout<<"Enter no of children:";    cin>>noch;   }

    int facin(int fc)
{     int c=0;
    ifstream x("facility.dat",ios::binary);
     while(x.read((char*)&fa,sizeof(fa)))
       if(fc==fa.ret_fc())  c++;
     if(c==0)
     {  cout<<" Facility code not found.Enter valid facility code\n";
	 return 0;}
     else
     return 1;
	}

       void add()
  {     int cd,p=sizeof(m);
     fstream x("member.dat",ios::binary|ios::in);
	  x.read((char*)&m,sizeof(m));
	  if(!x.fail())
	  { x.seekg(-p,ios::end);
	    x.read((char*)&m,sizeof(m));
	    cd=m.ret_mco();
	    x.close();
	    x.open("member.dat",ios::binary|ios::app);
	    m.in(++cd);
	    x.write((char*)&m,sizeof(m));
	    x.close();}
	    else {  cd=101;        x.close();
		    x.open("member.dat",ios::binary|ios::app);
		    m.in(cd);
		    x.write((char*)&m,sizeof(m));
		    x.close(); }
				  }

     void modify()
{    fstream x("member.dat",ios::binary|ios::in|ios::out);
     int cd,c=0,p=sizeof(m);
     cout<<"Enter member code to modify:";
     cin>>cd;
   while(x.read((char*)&m,sizeof(m)))
      {	if(cd==m.ret_mco())
	  {   m.out();
	    cout<<"Enter new data :";
	    ifstream y("fees.dat",ios::binary);
	    while(y.read((char*)&fe,sizeof(fe)))
		if(cd==fe.ret_mcode())
		{ m.in(cd,1);    c++; break;}              y.close();
	if(c==0)
	{ m.in(cd);    c++; }
	 x.seekp(-p,ios::cur);
	 x.write((char*)&m,sizeof(m));   }}

       if(c==0)
       cout<<"Member code not found\n";
       x.close();
				   }

   void delet()
   { int a,c=0;   char ch;
     ifstream x ("member.dat",ios::binary);
     ofstream y ("temp",ios::binary);
     cout<<"Enter member code to be deleted:";
     cin>>a;
     while( x.read((char*)&m,sizeof(m)))
	 if(a==m.ret_mco())
	 {     m.out();  c++;
	   cout<<"Confirm deletion Y/N:";     cin>>ch;
	   if(ch=='n'||ch=='N')
	   break;        }
	   else
	   y.write((char*)&m,sizeof(m));

	   if(c==0)
	   cout<<"Member code not found\n";

     x.close();   y.close();
     if(ch=='Y'||ch=='y')
      { remove("member.dat");
	rename("temp","member.dat");
	cout<<"Member deleted\n";  }
     else if(ch=='n'||ch=='N')
      cout<<"Member not deleted\n";           }

       void display()
  {  ifstream x ("member.dat",ios::binary|ios::in);
      int a,c=0;
cout<<"Enter member code for the member whose info is to be displayed:";
      cin>>a;
      while(x.read((char*)&m,sizeof(m)))
      {  if(a==m.ret_mco())
	 { m.out();  c++;
		 break;}  }
       if(c==0)
       cout<<"Member code not found\n";
       x.close();                           }

 void enf()
{   int cd,c=0;      Dt doj,dos;
   ofstream x("fees.dat",ios::binary|ios::app);
   cout<<"Enter member code:";    cin>>cd;
   ifstream y("member.dat",ios::binary);
   while(y.read((char*)&m,sizeof(m)))
	if(cd==m.ret_mco())
       {  c++;   doj=m.doj;
   xz:	  fe.in(cd);
	  dos=fe.ret_dos();
	  if(Dtcmp(doj,dos));
	  else { cout<<"Date of Submission invalid.Enter again\n";
		  goto xz;    }
	  x.write((char*)&fe,sizeof(fe));
	     }

	 if(c==0)
	 cout<<"Member code not found";
   x.close();  y.close();
}

void fdm()
{
ifstream x("fees.dat",ios::binary);
  int cd,c=0,d=0;
cout<<"Enter member code to be searched:";
cin>>cd;
ifstream y("member.dat",ios::binary);
while(y.read((char*)&m,sizeof(m)))
 if(cd==m.ret_mco())
 {  c++;
    while(x.read((char*)&fe,sizeof(fe)))
    if(fe.ret_mcode()==cd)
       {  fe.out();  d++;   }

       if(d==0)
	cout<<"Fee not deposited. Account not yet opened.\n";   }
if(c==0)
cout<<"Member code not found";
x.close(); y.close();
}

  void newf()
{ int cd,p=sizeof(fa);
  fstream x ("facility.dat",ios::binary|ios::in);
  x.read((char*)&fa,sizeof(fa));
   if(!x.fail())
    { x.seekg(-p,ios::end);
      x.read((char*)&fa,sizeof(fa));
      cd=fa.ret_fc();
      x.close();
      x.open("facility.dat",ios::binary|ios::app);
      fa.in(++cd);
      x.write((char*)&fa,sizeof(fa));
      x.close(); }
    else
       { cd=1;        x.close();
	 x.open("facility.dat",ios::binary|ios::app);
	 fa.in(cd);
	 x.write((char*)&fa,sizeof(fa));
	 x.close();}                               }

 void facd()
{ ifstream x("facility.dat",ios::binary);
  cout<<"Facility details:\n";
  while(x.read((char*)&fa,sizeof(fa)))
	 fa.out();
	 x.close();     }

void deletFacility()
{
	int a,c=0;   char ch;
     ifstream x ("facility.dat",ios::binary);
     ofstream y ("temp",ios::binary);
     cout<<"Enter facility code to be deleted:";
     cin>>a;
     while( x.read((char*)&fa,sizeof(fa)))
	 if(a==fa.ret_fc())
	 { c++;
	   cout<<"Confirm deletion Y/N:";     cin>>ch;
	   if(ch=='n'||ch=='N')
	   break;        }
	   else
	   y.write((char*)&fa,sizeof(fa));

	   if(c==0)
	   cout<<"Facility code not found\n";

     x.close();   y.close();
     if(ch=='Y'||ch=='y')
      { remove("facility.dat");
	rename("temp","facility.dat");
	cout<<"Facility deleted\n";  }
     else if(ch=='n'||ch=='N')
      cout<<"Facility not deleted\n";
}

void vert(int r1, int r2, int c)
{ for(int i=r1;i<=r2;i++)
 {gotoxy(c,i);
   cout<<"|";}       }

void horiz(int r1,int r2,int r)
{ for(int i=r1;i<=r2;i++)
  { gotoxy(i,r);
     cout<<"-"; }         }

void memlist()
{ clrscr();
date d;      getdate(&d);
int c=2;
vert(1,22,1);
horiz(2,80,1);
gotoxy(34,2);
cout<<"XYZ SPORTS CLUB\n";
gotoxy(30,3);
cout<<"ACIVITYWISE MEMBER LIST\n";
gotoxy(60,5);
cout<<"Date:"<<(int)d.da_day<<"/"<<(int)d.da_mon<<"/"<<d.da_year;
vert(1,22,80);
horiz(2,79,6);
gotoxy(c,7);
cout<<"S.";         gotoxy(c,8);  cout<<"No";
horiz(2,79,9);      c+=2;
vert(7,22,c);
gotoxy(++c,7);
cout<<"Memb";       gotoxy(c,8);  cout<<"Code";        c+=4;
vert(7,22,c);
gotoxy(++c+1,7);
cout<<"Member";     gotoxy(c+2,8);  cout<<"Name";         c+=10;
vert(7,22,c);
gotoxy(++c,7);
cout<<"Date of";    gotoxy(c,8);  cout<<"Joining";   c+=7;
vert(7,22,c);
gotoxy(++c+1,7);
cout<<"Address";    c+=10;
vert(7,22,c);
gotoxy(++c,7);
cout<<"Phone";      gotoxy(c,8);  cout<<"Number";   c+=6;
vert(7,22,c);
gotoxy(++c,7);
cout<<"Facility";   gotoxy(c+3,8);  cout<<"1";      c+=8;
vert(7,22,c);
gotoxy(++c,7);
cout<<"Facility";   gotoxy(c+3,8);  cout<<"2";     c+=8;
vert(7,22,c);
gotoxy(++c,7);
cout<<"Facility";   gotoxy(c+4,8);  cout<<"3";    c+=9;
vert(7,22,c);
gotoxy(++c,7);
cout<<"No of";      gotoxy(c,8);  cout<<"Child";
horiz(2,79,23);

ifstream x("member.dat",ios::binary);
int j=10,k=1,mcod;
while(x.read((char*)&m,sizeof(m)))
{  mcod=m.ret_mco();
   gotoxy(2,j);        cout<<k;
   gotoxy(5,j);        cout<<mcod;
   gotoxy(10,j);
		       int i=0;
		     while(m.mna[i]!='\0')
		     { for(;i<=9;++i)
		       cout<<m.mna[i];
		       if(i>9)  gotoxy(10,++j);
		       for(;m.mna[i]!='\0';++i)
		       cout<<m.mna[i];
		       if(i>5)  j--;    }


   gotoxy(21,j);       cout<<m.doj.dd<<'/'<<m.doj.mm<<'/';
   gotoxy(21,++j);     cout<<m.doj.yy;    j--;

   gotoxy(29,j);
			  i=0;
	       while(m.ads[i]!='\0')
	      { for(;i<=9;++i)
		cout<<m.ads[i];
		if(i==10) gotoxy(29,++j);
		if(i>9)
		for(;m.ads[i]!='\0';++i)
		cout<<m.ads[i];
		if(i>=10) j--;   }

		   gotoxy(40,j);
		      i=0;
		      for(;i<=5;++i)
		      cout<<m.phno[i];
		      if(i>5)  gotoxy(40,++j);
		      for(;m.phno[i]!='\0';++i)
		      cout<<m.phno[i];
		      if(i>5)  j--;

ifstream y("facility.dat",ios::binary);
while(y.read((char*)&fa,sizeof(fa)))
{      if(m.fc1==fa.ret_fc())
       {  gotoxy(47,j);  cout<<fa.fac;  }
       if(m.fc2==fa.ret_fc())
       {  gotoxy(56,j);	  cout<<fa.fac; }
       if(m.fc3==fa.ret_fc())
       {  gotoxy(65,j);	  cout<<fa.fac;}
					 }y.close();

      gotoxy(77,j);   cout<<m.noch;

					   j+=2;++k;        }
x.close();
getch();   }


void acmb()
{ date d;      getdate(&d);
int a;
facd();
cout<<"Enter Facility Code to see member list:";     cin>>a;
clrscr();
vert(1,18,1);
horiz(2,80,1);
gotoxy(34,2);
cout<<"XYZ SPORTS CLUB\n";
gotoxy(30,3);
cout<<"ACIVITYWISE MEMBER LIST\n";
gotoxy(55,5);
cout<<"Date:"<<(int)d.da_day<<"/"<<(int)d.da_mon<<"/"<<d.da_year;
vert(1,18,80);
horiz(2,79,6);
gotoxy(2,7);
cout<<" S.No";
horiz(2,79,8);
vert(7,18,8);
gotoxy(13,7);
cout<<"Activity";
vert(7,18,25);
gotoxy( 30,7);
cout<<"Member Code";
vert(7,18,43);
gotoxy(57,7);
cout<<"Member Name";
horiz(2,79,19);

ifstream x("facility.dat",ios::binary);
int j=9,k=1,fcod;
while(x.read((char*)&fa,sizeof(fa)))
{   if(a==fa.ret_fc())
     { 	 fcod=fa.ret_fc();
	  gotoxy(2,j);       cout<<k;
	  gotoxy(10,j);       cout<<fa.fac;

     ifstream y("member.dat",ios::binary);
     while(y.read((char*)&m,sizeof(m)))
	{ if(fcod==m.fc1||fcod==m.fc2||fcod==m.fc3)
	  { gotoxy(30,j);
	     cout<<m.ret_mco();
	     gotoxy(50,j);
	     cout<<m.mna;
	      ++j;  }}y.close();
				      ++j;++k;  }}
x.close();
getch();                  }

void Dtfee_details()
{
date d;    getdate(&d);
Dt e;
cout<<"Enter date to see fee details:";
inDt(e);
clrscr();
vert(1,18,1);
horiz(2,80,1);
gotoxy(35,2);
cout<<"XYZ SPORTS CLUB\n";
gotoxy(33,3);
cout<<"DATEWISE FEE DETAILS\n";
gotoxy(38,4);    cout<<e.dd<<'/'<<e.mm<<'/'<<e.yy;
gotoxy(60,5);
cout<<"Date:"<<(int)d.da_day<<"/"<<(int)d.da_mon<<"/"<<d.da_year;
vert(1,18,80);
horiz(2,79,6);
gotoxy(2,7);
cout<<" S.No";
horiz(2,79,8);
vert(7,19,8);
gotoxy(12,7);
cout<<"Date";
vert(7,19,20);
gotoxy( 23,7);
cout<<"Member Code";
vert(7,19,36);
gotoxy(43,7);
cout<<"Member name";
vert(7,19,60);
gotoxy(67,7);
cout<<"Amount";
ifstream x("fees.dat",ios::binary);
int j=9,k=1,mcod;  Dt dos;
while(x.read((char*)&fe,sizeof(fe)))
{         dos=fe.ret_dos();
	   if(Dtcmp(e,dos)==1)
	{  mcod=fe.ret_mcode();
	   gotoxy(2,j);       cout<<k;
	   gotoxy(9,j);
	   cout<<dos.dd<<"/"<<dos.mm<<"/"<<dos.yy;

     ifstream y("member.dat",ios::binary);
     while(y.read((char*)&m,sizeof(m)))
       {   if(mcod==m.ret_mco())
	   { gotoxy(25,j);
	     cout<<mcod;
	     gotoxy(40,j);
	     cout<<m.mna;
	     gotoxy(62,j);
	     cout<<fe.amount;
	      ++j;   }}y.close();
					++k;      }  }
x.close();
horiz(2,79,19);
getch();                }

void membcd()
{ date d;      getdate(&d);
int mcod,c=0;
ifstream y("member.dat",ios::binary);
cout<<"Enter member code:";    cin>>mcod;
clrscr();
while(y.read((char*)&m,sizeof(m)))
if(mcod==m.ret_mco())
{  c++;
vert(1,15,1);
horiz(2,80,1);
gotoxy(35,2);
cout<<"XYZ SPORTS CLUB\n";
gotoxy(35,3);
cout<<"MEMBERSHIP CARD\n";
gotoxy(65,4);
cout<<"Date:"<<(int)d.da_day<<"/"<<(int)d.da_mon<<"/"<<d.da_year;
gotoxy(2,5);
cout<<"Member Code:"<<mcod;
vert(1,15,80);
gotoxy(2,6);
cout<<"Name:"<<m.mna;
gotoxy(2,7);
cout<<"Address:"<<m.ads;
gotoxy(2,8);
cout<<"Phone:"<<m.phno;
gotoxy(20,8);
cout<<"Date of Joining"<<m.doj.dd<<"/"<<m.doj.mm<<"/"<<m.doj.yy;
ifstream x("facility.dat",ios::binary);
char f[3][100];
while(x.read((char*)&fa,sizeof(fa)))
{    if(m.fc1==fa.ret_fc())
       strcpy(f[0],fa.fac);
     if(m.fc2==fa.ret_fc())
       strcpy(f[1],fa.fac);
     if(m.fc3==fa.ret_fc())
       strcpy(f[2],fa.fac);      }
x.close();
gotoxy(2,9);
cout<<"Facilities Availed:"<<f[0]<<','<<f[1]<<','<<f[2];
gotoxy(2,10);
cout<<"Number of Children Allowed:"<<m.noch;

gotoxy(2,11);
cout<<"This card is valid for 2 years from date of joining"
    <<"after that it should be\n";
gotoxy(2,12);
cout<<"renewed.";
gotoxy(60,14);    cout<<"Authorised Signatory";
horiz(2,79,15);
	   }
if(c==0)
   cout<<"Member code not found";

   y.close();
   getch();}


void main()
{  clrscr();
      int ch1=0,ch2=0;
     while(ch1!=5)
 {       ch2=0;
     cout<<"\nMAIN MENU\n";
     cout<<"1.Member Processing\n"
	 <<"2.Fee Processing\n"
	 <<"3.Facility Processing\n"
	 <<"4.Reporting\n"
	 <<"5.Exit\n";
	 cout<<"Enter choice:";       cin>>ch1;

    switch(ch1)
   {  case 1:
	while(ch2!=5)
      { cout<<"\nMEMBER MENU\n";
	cout<<"1.New Member Registration\n"
	    <<"2.Member Information Modification\n"
	    <<"3.Deletion\n"
	    <<"4.Member Details\n"
	    <<"5.Return to main menu\n";
	    cout<<"Enter choice:";       cin>>ch2;
		 switch(ch2)
		 { case 1: add();      break;
		   case 2: modify();   break;
		   case 3: delet();    break;
		   case 4: display();  break;
		   case 5:             break;  }
						   } break;
      case 2:
	while(ch2!=3)
      { cout<<"\nFEE PROCESSING MENU\n";
	cout<<"1.Entry of fees\n"
	    <<"2.Fee details of a member\n"
	    <<"3.Return to main menu\n";
	    cout<<"Enter choice:";       cin>>ch2;
		 switch(ch2)
		 { case 1: enf();   break;
		   case 2: fdm();   break;
		   case 3:          break; }     }  break;

      case 3:
	while(ch2!=4)
      { cout<<"\nFACILITY PROCESSING MENU\n";
	cout<<"1.New facility\n"
	    <<"2.Facility details\n"
	    <<"3.Delete facility\n"
	    <<"4.Return to main menu\n";
	    cout<<"Enter choice:";       cin>>ch2;
		 switch(ch2)
		 { case 1: newf();   break;
		   case 2: facd();   break;
		   case 3: deletFacility();     break;
		   case 4: break; }           }break;

	case 4:
		while(ch2!=5)
      {    clrscr();
	cout<<"\nREPORTING MENU\n";
	cout<<"1.Member details\n"
	    <<"2.Activity details\n"
	    <<"3.Datewise fee details\n"
	    <<"4.Membership card\n"
	    <<"5.Return to main menu\n";
	    cout<<"Enter choice:";       cin>>ch2;
		 switch(ch2)
		 { case 1: memlist();          break;
		   case 2: acmb();             break;
		   case 3: Dtfee_details();    break;
		   case 4: membcd();           break;
		   case 5:             break; }
						   } break;

	case 5:         break; }       }

	getch();
		     }


