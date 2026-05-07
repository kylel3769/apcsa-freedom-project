this is for trinket.io

```
import pygame
import random

# import asyncio 

def main():  
    pygame.init()
    pygame.mixer.init()
    screen = pygame.display.set_mode((800, 600))
    font = pygame.font.SysFont("Arial", 18)
    
    closed = pygame.image.load("pc.png").convert_alpha()
    closed = pygame.transform.scale(closed, (200, 200)) 

    open = pygame.image.load("po.png").convert_alpha()
    open = pygame.transform.scale(open, (200, 200))

    enemy_location = "5" 
    toggle_button = closed.get_rect(topright=(800, 0))

    move = pygame.USEREVENT + 1
    pygame.time.set_timer(move, 5000)

    
    monitor_up = False
    current_cam = "1"
    running = True

    map_container = pygame.Rect(425, 250, 300, 230)

    cameras = {
        "1": {
            "safe": pygame.image.load("cam1.png").convert(),
            "evil": pygame.image.load("cam1evil.png").convert(),
            "rect": pygame.Rect(435, 260, 50, 30)
        },
        "2": {
            "safe": pygame.image.load("cam2.png").convert(),
            "evil": pygame.image.load("cam2evil.png").convert(),
            "rect": pygame.Rect(665, 260, 50, 30)
        },
        "3": {
            "safe": pygame.image.load("cam3.png").convert(),
            "evil": pygame.image.load("cam3evil.png").convert(),
            "rect": pygame.Rect(550, 360, 50, 30)
        },
        "4": {
            "safe": pygame.image.load("cam4.png").convert(),
            "evil": pygame.image.load("cam4evil.png").convert(),
            "rect": pygame.Rect(435, 440, 50, 30)
        },
        "5": {
            "safe": pygame.image.load("cam5.png").convert(),
            "evil": pygame.image.load("cam5evil.png").convert(),
            "rect": pygame.Rect(665, 440, 50, 30)
        }
    }
    
    home = pygame.image.load("cam0.png").convert()
    
    # got lazy
    home = pygame.transform.scale(home, (800, 600))
    
    toggle_button = pygame.Rect(600, 50, 200, 210) 

    while running:
        mc = pygame.mouse.get_pos()

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False
                
            if event.type == move_event:
                if random.randint(1, 2) == 1: 
                    if enemy_location == "1": enemy_location = random.choice(["2", "4"])
                    elif enemy_location == "2": enemy_location = random.choice(["1", "5"])
                    elif enemy_location == "4": enemy_location = random.choice(["1", "3"])
                    elif enemy_location == "5": enemy_location = random.choice(["2", "3"])
                    elif enemy_location == "3":
                        enemy_location = random.choice(["Office", "4", "5"])

            if event.type == pygame.MOUSEBUTTONDOWN:
                print(f'({mc[0]}, {mc[1]}, 60, 30)}}')
                
                if toggle_button.collidepoint(mc):
                    monitor_up = not monitor_up

                if monitor_up:
                    for cam_id, data in cameras.items():
                        if data["rect"].collidepoint(mc):
                            current_cam = cam_id

        screen.fill((0, 0, 0))
        screen.blit(home, (0, 0))

        if monitor_up:
            pygame.draw.rect(screen, (0, 0, 0), (50, 50, 700, 450))
            if current_cam == enemy_location:
                screen.blit(cameras[current_cam]["evil"], (60, 60))
            else:
                screen.blit(cameras[current_cam]["safe"], (60, 60))
       
       
       
            pygame.draw.rect(screen, (30, 40, 40), (50, 50, 700, 450), 5)   
            screen.blit(open, (600, 50))
            
            pygame.draw.rect(screen, (30, 30, 30), map_container)
            pygame.draw.rect(screen, (200, 200, 200), map_container, 2)
            
            line_color = (100, 100, 100)
            pygame.draw.line(screen, line_color, (485, 275), (665, 275), 3)
            pygame.draw.line(screen, line_color, (440, 290), (440, 440), 3)
            pygame.draw.line(screen, line_color, (675, 290), (675, 440), 3)
            pygame.draw.line(screen, line_color, (655, 450), (665, 450), 3)
            pygame.draw.line(screen, line_color, (655, 345), (655, 450), 3)
            pygame.draw.line(screen, line_color, (590, 345), (655, 345), 3)
            pygame.draw.line(screen, line_color, (590, 345), (590, 360), 3)
            pygame.draw.line(screen, line_color, (475, 370), (550, 370), 3)
            pygame.draw.line(screen, line_color, (475, 370), (475, 440), 3)
            pygame.draw.line(screen, line_color, (530, 380), (550, 380), 3)
            pygame.draw.line(screen, line_color, (530, 380), (530, 400), 3)
            
            sep_rm = pygame.Rect(500, 400, 150, 70)
            pygame.draw.rect(screen, (150, 150, 150), sep_rm)
            sep = font.render("Sep Room", True, (0, 0, 0))
            screen.blit(sep, (550, 420))
    
            for cam_id, data in cameras.items():
                is_active = current_cam == cam_id
                color = (255, 255, 255) if is_active else (80, 80, 80)
                pygame.draw.rect(screen, color, data["rect"])
                
                label = font.render(cam_id, True, (0, 0, 0))
                screen.blit(label, (data["rect"].x + 18, data["rect"].y + 5))


        else:
            screen.blit(closed, (600, 50))


        pygame.display.flip()

    pygame.quit()

main()

```
