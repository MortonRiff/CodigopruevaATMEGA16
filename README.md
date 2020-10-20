# CodigopruevaATMEGA16
enciende y apaga un led


 .def gen  =r16
 .def gen2 =r17
 .def gen3 =r18
 .def PB   =r19

 .cseg

     ldi  r16, high(ramend)
     out  SPH, r16
     ldi  r16, low(ramend)
     out  SPL, r16
     ldi  gen, 0x00
     out  DDRA, gen
     ldi  gen, 0x01
     out DDRC, gen

loop: in PB, PORTA
      cpi PB, 0x00
      brne led
      rjmp loop

led:  ldi gen, 0x01
      out PORTC, gen
      rcall tiempo
      ldi gen, 0x00
      out DDRC, gen
      ret

tiempo: ldi gen, 0x01
d1:     ldi gen2, 0x01
d2:     ldi gen3, 0x01
d3:     dec gen3
        brne   d3
        dec   gen2
        brne   d2
        dec   gen
        brne   d1
        ret 
