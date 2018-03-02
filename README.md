# WebGL Water Demo

http://madebyevan.com/webgl-water/

1)water.js is a "water texture"　that stores (height, y-velocity, normal) of water surface

2)renderer.js 

waterShader is doing ray-tracing:
    ray = surfacePoint - eye
    reflectedRay = reflect(ray, surfacePointNormal)
    refractedRay = refract(ray, surfacePointNormal, n_air/n_water)
    Calculated the intersectPoint with Cube, sample the color on Cube(getWallColor), which composes tileColor and causticsColor
    
causticsShader is generating causticsTex, 
    There is a light-wave-front mesh.
    vertexShader calculates oldPos and newPos for each vertex, which is the mesh point projected along ray and refractedRay.
    oldArea = dFdx(oldPos) * dFdy(oldPos)
    newArea = dFdx(newPos) * dFdy(newPos)
    fragmentShader gl_FragColor = (newArea / oldArea, 0, 0, 1)
    
    what is the texture point for a vertex?
    how to sample causticsTex?
