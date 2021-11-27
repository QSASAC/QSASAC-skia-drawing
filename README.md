# QSASAC-skia-drawing
import skia
import contextlib
from IPython.display import display, Image
import random

color1 = skia.Color(random.randint(0, 255), random.randint(0, 255), random.randint(0, 255))
color2 = skia.Color(random.randint(0, 255), random.randint(0, 255), random.randint(0, 255))
color3 = skia.Color(random.randint(0, 255), random.randint(0, 255), random.randint(0, 255))
color4 = skia.Color(random.randint(0, 255), random.randint(0, 255), random.randint(0, 255))
count = 0

@contextlib.contextmanager
def draw_target():
    global count
    surface = skia.Surface(256, 256)
    with surface as canvas:
        yield canvas
    image = surface.makeImageSnapshot()
    display(Image(data=image.encodeToData()))
    image.save("output{}.png".format(count) , skia.kPNG)
    count = count +1

with draw_target() as canvas:
    canvas.drawColor(skia.ColorWHITE)
    
    paint = skia.Paint(
        
        Shader=skia.GradientShader.MakeLinear(
        points=[(0.0, 0.0), (256.0, 256.0)],
        colors=[color1, color2, color3, color4]),
        
        Style=skia.Paint.kStroke_Style,
        StrokeWidth=8,
        
        AntiAlias=True,
        StrokeCap=skia.Paint.kRound_Cap
        )
        
    path = skia.Path()
    path.moveTo(10, 10)
    path.quadTo(256, 64, 128, 128)
    path.quadTo(10, 192, 250, 250)
    canvas.drawPath(path, paint)

with draw_target() as canvas:
    canvas.drawColor(skia.ColorWHITE)
    
    paint = skia.Paint(
        
        Shader=skia.GradientShader.MakeLinear(
        points=[(0.0, 0.0), (128.0, 128.0)],
        colors=[color1, color2, color3, color4]),
        
        Style=skia.Paint.kFill_Style,
        AntiAlias=True,
        StrokeWidth=4,
        )
    
    rect = skia.Rect.MakeXYWH(64, 64, 100, 100)
    canvas.drawRect(rect, paint)

with draw_target() as canvas:
    canvas.drawColor(skia.ColorWHITE)
    
    paint = skia.Paint(
        
        Shader=skia.GradientShader.MakeLinear(
        points=[(0.0, 0.0), (256.0, 256.0)],
        colors=[color1, color2, color3, color4]),
        
        Style=skia.Paint.kFill_Style,
        AntiAlias=True,
        StrokeWidth=4,
        )
    
    canvas.drawCircle(128, 128, 50, paint)
