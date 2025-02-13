#define LATCH_PIN 4
#define CLK_PIN 7
#define DATA_PIN 8


const char SEGMENT_MAP_DIGIT[] = {0xC0,0xF9,0xA4,0xB0,0x99,0x92,0x82,0xF8,0X80,0X90};

	
	

/* Byte maps to select segment 1 to 4 */
const char SEGMENT_SELECT[] = {0xF1,0xF2,0xF4,0xF8,0xff,0xf0};
	



/* Write a value to one of the 4 digits of the display */
unsigned short int contador_display = 0;

void setup() {
  // put your setup code here, to run once:
  pinMode(LATCH_PIN,OUTPUT);
   pinMode(CLK_PIN,OUTPUT);
    pinMode(DATA_PIN,OUTPUT);

}

void loop() {
  // put your main code here, to run repeatedly:
  int valor = 1999;
  
  SevenSeg_WriteValueToSegment(&valor);
  
}

void SevenSeg_WriteValueToSegment(unsigned int *value){
  
	int seguimentos_individuais[4];  //converte um valor numérico para quatro digitos individuais
	seguimentos_individuais[0] = *value / 1000;
	seguimentos_individuais[1] = (*value / 100) % 10;
	seguimentos_individuais[2] = (*value / 10) % 10;
	seguimentos_individuais[3] = *value % 10;

	
	char auxi_seguimento, aux_segment_select; //variáveis auxíliares controle dos displays de sete seguimentos

	auxi_seguimento = (SEGMENT_MAP_DIGIT[seguimentos_individuais[contador_display]]); //mapea os seguimentos que serão habilitados através do ponteiro
	
	aux_segment_select = SEGMENT_SELECT[contador_display];  //seleciona o seguimento que será habilitado momentâneamente

	

   digitalWrite(LATCH_PIN,1);
	for (uint8_t i = 0; i < 8; i++)  {
    digitalWrite(DATA_PIN,(auxi_seguimento & (1 << (7 - i))));
    digitalWrite(CLK_PIN,1);
    digitalWrite(CLK_PIN,0);
	}

	for (uint8_t i = 0; i < 8; i++) {
	
    digitalWrite(DATA_PIN,(aux_segment_select & (1 << (7 - i))));
    digitalWrite(CLK_PIN,1);
    digitalWrite(CLK_PIN,0);
		
		}
     digitalWrite(LATCH_PIN,0);

	contador_display++;
	if(contador_display==4){
		contador_display = 0;
	}
	
}
