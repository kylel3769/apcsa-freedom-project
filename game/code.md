this is for trinket.io

```
import pygame
# import asyncio


# async def main():
def main():  
    pygame.init()
    screen = pygame.display.set_mode((800, 600))

    monitor_up = False
    cam = 1
    running = True

    cam1_button = pygame.Rect(600, 400, 80, 40)
    cam2_button = pygame.Rect(600, 450, 80, 40)
    toggle_button = pygame.Rect(300, 550, 200, 30)

    while running:
        mouse_pos = pygame.mouse.get_pos()

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False

            if event.type == pygame.MOUSEBUTTONDOWN:
                if toggle_button.collidepoint(mouse_pos):
                    monitor_up = not monitor_up

                if monitor_up:
                    if cam1_button.collidepoint(mouse_pos):
                        cam = 1
                    if cam2_button.collidepoint(mouse_pos):
                        cam = 2

        screen.fill((0, 0, 0))

        if monitor_up:
            if cam == 1:
                pygame.draw.rect(screen, (0, 100, 0), (50, 50, 700, 350))
            else:
                pygame.draw.rect(screen, (100, 0, 0), (50, 50, 700, 350))

            pygame.draw.rect(screen, (200, 200, 200), cam1_button)
            pygame.draw.rect(screen, (200, 200, 200), cam2_button)
        else:
            pygame.draw.circle(screen, (100, 100, 100), (400, 300), 80)

        pygame.draw.rect(screen, (50, 50, 255), toggle_button)

        pygame.display.flip()
        # await asyncio.sleep(0)


# asyncio.run(main())
main()
```
