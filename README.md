# 2.8 oled initial code
some initial code for oled/lcd display moudle

uint16  S6E63D6_Init_Data[]={

   0x02,0x0000, 

   0x03,0x0030, 

   0x10,0x0000,

   0x18,0x0028,

   0xf8,0x000f,

   0xf9,0x000f,

   0x05,0x0001,

   

   0x70,0x2580, 

   0x71,0x2780,

   0x72,0x3380,

   0x73,0x1d80,

   0x74,0x1f11,

   0x75,0x2419,

   0x76,0x1a14,

   0x77,0x211a,

   0x78,0x2013,

 

   };

   

static void delay10ms(void)

{

 uint16 i;

 i=10000;

 while(i--);

}

   

 

void OLED_init(void)      {

 uint32 i;

 uint16 temp;

   uint16 *Pointer;

 OLED_RST_LOW;

   delay10ms();         //Keep more time to read MTP value

 OLED_RST_HI;

   delay10ms();         //Keep more time to read MTP value

 

 temp=sizeof(S6E63D6_Init_Data)/2;

 WriteCMD(0x23);

 

 for(i=0;i<(temp); )

  {

  WriteCMD(S6E63D6_Init_Data[i++]);

  WriteData(S6E63D6_Init_Data[i++]);

 

  }

 while(1)

 {

  WriteCMD(0x22);

   Pointer= (uint16 *)Pic_01;

 for(i=0;i<(320*240);i++)< span="">

 {

  WriteData(*Pointer++);

 }

   for(i=0;i<1000000;i++);< span="">

  WriteCMD(0x22);

   Pointer= (uint16 *)Pic_02;

 for(i=0;i<(320*240);i++)< span="">

 {

  WriteData(*Pointer++);

 }

 for(i=0;i<1000000;i++); 

 }

}

 

//    end

 
