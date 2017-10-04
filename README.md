# game.py
import pygame
import sys
from pygame.locals import*
from random import*
import os
pygame.init()
fuente = pygame.font.Font(None, 20)	
screen = pygame.display.set_mode((800,600))
sprite_link = pygame.image.load(os.path.join("imagen", "listSpritex2.png"))
color3 = pygame.Color(255,255,255)
velocidadx = 0
velocidady = 0
posx = 0
posy = 100
sprite_section = (0, 0, 31, 33)
move = "down"
movement = False
s = 0

while True:

	superficie = pygame.Surface((100,100))
	superficie.blit(sprite_link, (0,0), sprite_section)
	ubicacionx = str(posx)
	ubicaciony = str(posy)
	mensaje = fuente.render(str(s),1,color3)
	mensaje2 = fuente.render(ubicaciony,1,color3)


	screen.fill((0,0,0))
	screen.blit(superficie,(posx,posy))

	posx += velocidadx
	posy += velocidady

	for evento in pygame.event.get():

		if evento.type == QUIT:
			pygame.quit()
			sys.exit()
		elif evento.type == pygame.KEYDOWN:
			if evento.key == pygame.K_LEFT:
				velocidadx = -0.2
				move = "left"
				movement = True
				s=0
				
				
			elif evento.key == pygame.K_RIGHT:
				velocidadx = +0.2
				move = "right"
				movement = True
				s=0

			
			elif evento.key == pygame.K_UP:
				velocidady = -0.2
				move = "up"
				movement = True
				s=0
				
			elif evento.key == pygame.K_DOWN:
				velocidady = 0.2
				move = "down"
				movement = True
				s=0

		elif evento.type == pygame.KEYUP:
			if evento.key == pygame.K_LEFT and not pygame.key.get_pressed()[K_RIGHT]:
				velocidadx = 0
				if not (pygame.key.get_pressed()[K_RIGHT] or pygame.key.get_pressed()[K_LEFT]):
					movement = False
				
			elif evento.key == pygame.K_RIGHT and not pygame.key.get_pressed()[K_LEFT]:
				velocidadx = 0
				if not (pygame.key.get_pressed()[K_RIGHT] or pygame.key.get_pressed()[K_LEFT]):
					movement = False
				
			elif evento.key == pygame.K_UP and not pygame.key.get_pressed()[K_DOWN]:
				velocidady = 0
				if not (pygame.key.get_pressed()[K_UP] or pygame.key.get_pressed()[K_DOWN]):
					movement = False
				
			elif evento.key == pygame.K_DOWN and not pygame.key.get_pressed()[K_UP]:
				velocidady = 0
				if not (pygame.key.get_pressed()[K_UP] or pygame.key.get_pressed()[K_DOWN]):
					movement = False
	# animacion
	down = [(0, 0, 31, 33), (0, 59, 31 , 33)]
	up = [(122, 0, 31 ,33), (122, 59 ,31, 33)]
	left = [(59, 0, 31, 33), (59, 59, 31, 33)]
	right = [(180, 0 ,31, 33), (180, 59 , 31, 33)]
	if movement:
		if move == "down":
			if round(s)%2==0:
				sprite_section = down[0]
			else:
				sprite_section = down[1]
		elif move == "up":
			if round(s)%2==0:
				sprite_section = up[0]
			else:
				sprite_section = up[1]
		elif move == "left":
			if round(s)%2==0:
				sprite_section = left[0]
			else:
				sprite_section = left[1]
		elif move == "right":
			if round(s)%2==0:
				sprite_section = right[0]
			else:
				sprite_section = right[1]
		s += 0.005




	screen.blit(mensaje,(0,0))
	screen.blit(mensaje2,(0,10))

	pygame.display.update()
